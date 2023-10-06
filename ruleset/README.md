#### rules

类型,参数,策略(,no-resolve)

TYPE,ARGUMENT,POLICY(,no-resolve)

no-resolve 选项是可选的, 它用于跳过规则的 DNS 解析. 当您想要使用 GEOIP、IP-CIDR、IP-CIDR6、SCRIPT 规则, 但又不想立即将域名解析为 IP 地址时, 这个选项就很有用了.

>DOMAIN-SUFFIX：域名后缀匹配
>
>DOMAIN：域名匹配
>
>DOMAIN-KEYWORD：域名关键字匹配
>
>IP-CIDR：IP 段匹配
>
>SRC-IP-CIDR：源 IP 段匹配
>
>GEOIP：GEOIP 数据库（国家代码）匹配
>
>DST-PORT：目标端口匹配
>
>SRC-PORT：源端口匹配
>
>PROCESS-NAME：源进程名匹配
>
>RULE-SET：Rule Provider 规则匹配
>
>MATCH：全匹配



#### Rule Providers 规则集

```yaml
rule-providers:
  apple:
    behavior: "domain" # domain, ipcidr or classical (仅限 Clash Premium 内核)
    type: http
    url: "url"
    # format: 'yaml' # or 'text'
    interval: 3600
    path: ./apple.yaml
  microsoft:
    behavior: "domain"
    type: file
    path: /microsoft.yaml

rules:
  - RULE-SET,apple,REJECT
  - RULE-SET,microsoft,policy
```

有两种语法格式和三种行为类型可用，yaml语法可以先写在txt中。

##### domain

```yaml
payload:
  - '.blogger.com'
  - '*.*.microsoft.com'
  - 'books.itunes.apple.com'
```

```txt
# comment
.blogger.com
*.*.microsoft.com
books.itunes.apple.com
```

##### ipcidr

```yaml
payload:
  - '192.168.1.0/24'
  - '10.0.0.0.1/32'
```

```txt
# comment
192.168.1.0/24
10.0.0.0.1/32
```

##### classical

```yaml
payload:
  - DOMAIN-SUFFIX,google.com
  - DOMAIN-KEYWORD,google
  - DOMAIN,ad.com
  - SRC-IP-CIDR,192.168.1.201/32
  - IP-CIDR,127.0.0.0/8
  - GEOIP,CN
  - DST-PORT,80
  - SRC-PORT,7777
  # MATCH 在这里并不是必须的
```

```txt
# comment
DOMAIN-SUFFIX,google.com
DOMAIN-KEYWORD,google
DOMAIN,ad.com
SRC-IP-CIDR,192.168.1.201/32
IP-CIDR,127.0.0.0/8
GEOIP,CN
DST-PORT,80
SRC-PORT,7777
```


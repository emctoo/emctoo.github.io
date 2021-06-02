# CFSSL

cloudflare的TLS/SSL工具。包含命令行工具和HTTP API服务。

命令行工具:

- cfssl
- multirootca
- mkbundle
- cfssljson

```shell
export CFSSL_URL="https://pkg.cfssl.org/R1.2"
wget "${CFSSL_URL}/cfssl_linux-amd64" -O /usr/local/bin/cfssl
wget "${CFSSL_URL}/cfssljson_linux-amd64" -O /usr/local/bin/cfssljson
chmod +x /usr/local/bin/cfssl /usr/local/bin/cfssljson
```

#### 创建CA

```shell
# cat ca-csr.json
{
  "CN": "example.com",
  "key": {
    "algo": "rsa",
	"size": 2048
  },
  "names": [{
    "C": "CN",
    "ST": "Sichuan",
    "L": "Chengdu",
    "O": "Kubernetes",
    "OU": "system"
  }]
}
```

- CN: Common Name，浏览器使用该字段验证网站是否合法，一般为域名。
- C: Country
- ST: State，州，省
- L: Locality, 地区，城市
- O: Organization Name, 组织名称，公司名称
- OU: Organization Unit Name，组织单位名称，公司部门

#### 打包证书

根据上面的配置，生成 `ca.csr`, `ca-key.pem`, `ca.pem` 三个文件

```shell
# cfssl gencert -initca ca-csr.json | cfssljson -bare ca
```

```shell
# cat ca-config.json 
{
  "signing": {
    "default": {
	  "expiry": "87600h"
	},
	"profiles": {
	  "example.com": {
	    "usages": ["signing", "key encipherment", "server auth", "client auth"],
		"expiry": "87600h"
	   }
	}
  }
}
```

- default: default policy, set expiercy to 1 year (8760 hours)

生成 `example.com` 的证书

```shell
# cfssl gencert -ca=ca.pem -ca-key=ca-key.pem -config=ca-config.json -profile=example.com ca-csr.json | cfssljson -bare example.com
```


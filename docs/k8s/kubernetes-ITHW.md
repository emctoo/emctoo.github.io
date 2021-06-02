## kubernetes in the hard way

查看依赖的版本

```shell
kubeadm config images list
```

kube相关的是和k8s的版本一致的，其他的 etcd 需要查看

### 证书签发

```sh
export CFSSL_URL="https://pkg.cfssl.org/R1.2"
wget "${CFSSL_URL}/cfssl_linux-amd64" -O /usr/local/bin/cfssl
wget "${CFSSL_URL}/cfssljson_linux-amd64" -O /usr/local/bin/cfssljson
wget "${CFSSL_URL}/cfssl-certinf_linux-amd64" -O /usr/local/bin/cfssl-certinfo
chmod +x /usr/local/bin/cfssl /usr/local/bin/cfssljson /usr/local/bin/cfssl-certinfo
```



### etcd部署

### master部署

需要部署 kube-apiserver kube-controller-manager, kube-scheduler, etcd

### node部署

需要部署 kubelet, kube-proxy, CRI, etcd

### 网络部署
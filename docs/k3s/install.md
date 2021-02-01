### server installation

air-gap install

image file, example: (version **1.20.2+k3s1**)

```
https://github.com/k3s-io/k3s/releases/download/v1.20.2%2Bk3s1/k3s-airgap-images-amd64.tar
```

```shell
sudo mkdir -p /var/lib/rancher/k3s/agent/images/
sudo cp ./k3s-airgap-images-$ARCH.tar /var/lib/rancher/k3s/agent/images/
```

- Place the k3s binary at `/usr/local/bin/k3s` and ensure it is executable

```shell
https://github.com/k3s-io/k3s/releases/download/v1.20.2%2Bk3s1/k3s
```

- install script

```shell
wget https://get.k3s.io -O install.sh
```

- install server node

```shell
INSTALL_K3S_SKIP_DOWNLOAD=true INSTALL_K3S_EXEC="--write-kubeconfig-mode 666 --tls-san 192.168.100.201 --node-external-ip=192.168.100.201" ./install.sh
# notice the external IP, from [1]
```

[1]: https://github.com/k3s-io/k3s/issues/1523	"unable to connect agent to master"

- on the server node, get the token at `/var/lib/rancher/k3s/server/node-token`
- install on worker node

```
INSTALL_K3S_SKIP_DOWNLOAD=true K3S_URL=https://192.168.100.201:6443 K3S_TOKEN=mynodetoken ./install.sh
```



### 卸载

server node  run

```shell
/usr/local/bin/k3s-uninstall.sh
```

worker node run

```shell
/usr/local/bin/k3s-agent-uninstall.sh
```


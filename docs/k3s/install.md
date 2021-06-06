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
sudo cp k3s /usr/local/bin/
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

```shell
sudo cat /var/lib/rancher/k3s/server/node-token
```

- install on worker node

```
INSTALL_K3S_SKIP_DOWNLOAD=true K3S_URL=https://192.168.100.201:6443 K3S_TOKEN=$TOKEN ./install.sh
```

#### server node

```
rm -rf $HOME/.kube

mkdir -p $HOME/.kube
sudo cp -i /etc/rancher/k3s/k3s.yaml $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```



#### registry 问题

https://rancher.com/docs/k3s/latest/en/installation/private-registry/

k3s 默认使用containerd做cri，启动时候会去找 `/etc/rancher/k3s/registries.yaml`，根据mirrors字段生成containerd的配置。

```yaml
# /etc/rancher/k3s/registries.yaml
mirrors:
  "docker.io":
    endpoint:
      - "https://fhnbkhe7.mirror.aliyuncs.com"
      - "https://registry-1.docker.io"
```

可以在 `/var/lib/rancher/k3s/agent/etc/containerd/config.toml` 下找到containerd相关的配置。

问题：k3s 中containerd相关的配置在什么地方？

另外的，关于如何使用私有镜像的教程： https://www.cnblogs.com/yaopengfei/p/13705822.html。

(注意的是，阿里云的私有镜像，在界面上要使用旧版的才能进行文中进行的操作。)

### 卸载

server node  run

```shell
/usr/local/bin/k3s-uninstall.sh
```

worker node run

```shell
/usr/local/bin/k3s-agent-uninstall.sh
```

#### containerd

[configure image registry](https://github.com/containerd/cri/blob/master/docs/registry.md)

containerd 的默认配置在 `/etc/containerd/config.toml`（k3s的实现增加了抽象层）

k3s 中 socket address: `/run/k3s/containerd/containerd.sock`

#### runc



#### aliyun container service

需要RAM授权

URL: https://cs.console.aliyun.com/

基本的办法只能是把镜像做成是"公有类型"



server node 上的 registries.yaml is not respected.


```shell
kubeadm config images list # 需要pull的镜像
kubeadm config images pull # pull 需要的所有 image
```

```shell
kubeadm config print init-defaults > kubeadm-config.yaml
```

修改 `kubeadm-config.yaml`

- localAPIEndpoint.advertiseAddress: 192.168.8.65
- networking.podSubnet: 10.244.0.0/16

podSubnet 的 10.244.0.0/16 是 flannel的默认网络

imageRepository 可以配置成本地的 registry

```shell
kubeadm init --config=kubeadm-config.yaml | tee kubeadm-init.log
```

```shell
kubeadm reset
```

flannel 的网络重启下就可以了



[validate cluster](https://opensource.com/article/20/6/kubernetes-raspberry-pi)


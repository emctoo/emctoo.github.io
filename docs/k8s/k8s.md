### namespace

同一个 cluster 下的命名空间，不同的project, team, or customers to share the same cluster.

- a scope of Names，名字在同一个ns上不能重复，但是不同之间的可以重复。
- a mechanism to attach authorization and policy  to a subsection of the cluster. 在 cluster 的一部分上应用权限机制。

namespace 和 context 有什么关系？

```yaml
# hello-ns.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: hello
```

```shell
kubectl create -f hello-ns.yaml
```

```
kubectl delete namespace hello
```

Set namespace:

```shell
# set kubectl default namespace
kubectl config set-context --current --namespace=hello
# validate it
kubectl config view --minify | grep namespace
```

- kubectl 直接copy binary 就可以，默认配置文件 $HOME/.kube/config
- kubectl api-resources 可以列出所有的资源列表


### service

static ip、load balance、service discovery



**[TODO]** [K8S 私有镜像](https://kirakirazone.com/2020/08/06/k8s%E6%8B%89%E5%8F%96%E7%A7%81%E6%9C%89%E9%95%9C%E5%83%8F/) 引入的方式

kubectl run 可以直接运行pod `kubectl help run`
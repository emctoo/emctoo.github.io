### namespace

同一个 cluster 下的命名空间，不同的project, team, or customers to share the same cluster.

- a scope of Names，名字在同一个ns上不能重复，但是不同之间的可以重复。
- a mechanism to attach authorization and policy  to a subsection of the cluster. 在 cluster 的一部分上应用权限机制。

namespace 和 context 有什么关系？



Set namespace:

```shell
kubectl config set-context --current --namespace=<insert-namespace-name-here>
# Validate it
kubectl config view --minify | grep namespace:
```


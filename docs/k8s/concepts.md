## kubernetes concpets

#### contex

关于context: [Configure Access to Multiple Clussters](https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/)

一般情况下 cluster 和 context 对应的。

kubectx 命令

[更多 context 切换等的介绍](https://tonybai.com/2019/08/31/kubectl-productivity-part3/)

#### namespace

#### workloads

pod是基本的构成单元。

workload resources 用 controllers 来管理pod

- Deployment and ReplicaSet
- StatefulSet
- DaemonSet
- Job and CronJob
- CRD: custom resource definition

#### service, load balancing and networking

#### storage

#### configuration

#### security

#### policies

#### scheduling and eviction
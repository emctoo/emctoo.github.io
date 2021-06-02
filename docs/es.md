## Elasticsearch

![img](S:\emctoo.github.io\docs\assets\es-kg.png)

### shard & replica

- index 包含多个shared，默认5个，创建时候确定。
- document存在primary shard
- replica shard: primary shard 的copy，default is 1, increase search performance and for fail-over, 不能再同一个节点上，随时修改
- 每个shard是最小工作单元，承载部分数据，lucene实例，完整的建立索引和处理请求的能力
- 增减节点是，shard会自动在nodes中负载均衡
- primary shard 和自己的replica shard不能放在同一个节点上，否则起不到容错的作用。

### 工具

kibana [stack monitoring](https://www.elastic.co/guide/en/kibana/current/xpack-monitoring.html)

Elastic-HQ 和 cerebro

### 监控性能指标

节点运行状况: CPU, memory, disk: [Node stats API](https://www.elastic.co/guide/en/elasticsearch/reference/current/cluster-nodes-stats.html)

```shell
curl :9200/_node/stats | jq ".nodes[] | {os: .os, fs: .fs}"
```

JVM: heap, GC, threads, buffer pool:

```shell
curl :9200/_nodes/stats | jq ".nodes[].jvm"
```

cluster health: shards and nodes

分片过多或者过少都会引发问题：

```
分片数量过多，则批量写入/查询请求被分割为过多的子写入/查询，导致该索引的写入、查询拒绝率上升；
对于数据量较大的索引，当分片数量过小时，无法充分利用节点资源，造成机器资源利用率不高或不均衡，影响写入/查询的效率。
```

[cluster stats api](https://www.elastic.co/guide/en/elasticsearch/reference/current/cluster-health.html)

```http
GET /_cluster/health
```

其中：

- Count of Active Shards：活动分片计数。集群中活动分片的数量。 
- relocating_shards：重定位分片，由于节点丢失而移动的分片计数。
- initializing_shards：初始化分片，由于添加索引而初始化的分片计数。 
- unassigned_shards：未分配的分片，尚未创建或分配副本的分片计数。
- delayed_unassigned_shards： timeout 决定的延迟分配的shard

#### query 性能：QPS and delay

请求分成两个阶段：

- query phase, cluster将请求分发到索引中的每个shard (primary / replica shards)
- fetch phase, 查询结果的收集、处理并返回给用户。

[index stats api](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-stats.html)

```http
GET /<target>/_stats/<index-metric>
```

#### index 性能：refresh and merge

文档增删改后，cluster 需要更新索引，然后在每个节点上刷新。用户只能控制 refresh interval。

增删改会形成 segment 并刷新到 disk，并且每个segment小号资源，cluster会将较小的合并成更大的segment 提升性能。索引速率 (indexing rate) 和合并时间 (merge time) 是重要的参考 metrics。

[documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/cluster-nodes-stats.html)

```sh
curl -v :9200/_node/stats | jq ".nodes[].indices"
```


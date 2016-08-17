# Target
测试RabbitMQ集群Exchange 个数对性能影响

------

# 测试环境
- 服务器配置

| Node | OS | CPU | MEM | DISK |
|------|----|-----|-----|------|
|node1|CentOS Linux release 7.1.1503 (Core)|24 X 2599.968|32GB|250GB HDD|
|node2|CentOS Linux release 7.1.1503 (Core)|24 X 2599.968|32GB|250GB HDD|
|node3|CentOS Linux release 7.1.1503 (Core)|24 X 2599.968|32GB|250GB HDD|

- RabbitMQ服务配置

| Type | Value| 
|------|------|
| RabbitMQ 版本| 3.6.1 |
| Erlang 版本| 16B |
| Exchange 模式| N topic exchanges -> 1 queue|
| Consumer ack | True|
| 消息大小| 20B |
| 消息持久化| True |

--------

# 测试数据

- **3个节点，no mirror HA 1个exchange**

![3node_exch1](https://github.com/barryz/rabbitmq-bench/blob/master/imgcaches/ex_perf_exch1.png "3node_exch1")


- **3个节点，no mirror HA 3个exchange**

![3node_exch3](https://github.com/barryz/rabbitmq-bench/blob/master/imgcaches/ex_perf_exch3.png "3node_exch3")


- **3个节点，no mirror HA 5个exchange**

![3node_exch5](https://github.com/barryz/rabbitmq-bench/blob/master/imgcaches/ex_perf_exch5.png "3node_exch5")


- **3个节点，no mirror HA 6个exchange**

![3node_exch6](https://github.com/barryz/rabbitmq-bench/blob/master/imgcaches/ex_perf_exch6.png "3node_exch6")

----------

# 数据汇总

|Exchange数|Cluster with 3 nodes|
|------|------------|
|1| 24000/23731|
|3| 61296/61292|
|5| 96000/95888|
|6| 105913/105928|

---------------

# 结论
  - 单个exchange QPS上限为24000左右。
  - 叠加exchange 可以成正比增加集群性能。
  - 集群3个节点情况下，达到11W QPS后，很多connections处于flow control状态。
  - 10W 左右的QPS为集群的性能瓶颈点。

# Target
测试RabbitMQ集群设置Mirror Queue前后的性能

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
| Exchange 模式| 1 topic exchange -> 1 queue|
| Consumer ack | True|
| 消息大小| 20B |
| 消息持久化| True |

--------

# 测试数据

- **2个节点，no mirror HA**

![2node_noha](https://github.com/barryz/rabbitmq-bench/blob/master/imgcaches/N2Q1E1TC20P10T300PRE100.png "2node_noha")


- **2个节点，mirror HA with 2 nodes**

![2node_ha](https://github.com/barryz/rabbitmq-bench/blob/master/imgcaches/N2Q1E1TC20P10T300PRE100_HA2.png "2node_ha")


- **3个节点，no mirror HA**

![3node_noha](https://github.com/barryz/rabbitmq-bench/blob/master/imgcaches/N3Q1E1TC20P10T300PRE100.png "3node_noha")


- **3个节点， mirror HA with 2 nodes**

![3node_2ha](https://github.com/barryz/rabbitmq-bench/blob/master/imgcaches/N3Q1E1TC20P10T300PRE100_HA2.png "3node_2ha")


- **3个节点， mirror HA with 3 nodes**

![3node_3ha](https://github.com/barryz/rabbitmq-bench/blob/master/imgcaches/N3Q1E1TC20P10T300PRE100_HA3.png "3node_3ha")


----------

# 数据汇总

|节点数| clustering | cluster HA 2 nodes | cluster HA 3 nodes|
|------|------------|--------------------|-------------------|
|2| 23985/23594|19566/19192| |
|3| 24000/23731|19200/19024|19502/19267|

---------------

# 结论
  - mirror HA 模式下，集群性能下降30% 左右。
  - 非mirror HA 模式，集群节点数增加并未增加集群吞吐量。
  - mirror HA 模式下， mirror 2 nodes 和 3 nodes 性能差不不大。 


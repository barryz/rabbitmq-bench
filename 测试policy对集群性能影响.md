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
| RabbitMQ 版本| 3.6.1 |
| Erlang 版本| 16B |
| Exchange 模式| 1 topic exchange -> 1 queue|
| Consumer ack | True|
| 消息大小| 20B |
| 消息持久化| True |

以下有HA 测试的环境均为: queue mirrored 2 nodes.

--------

# 测试数据

- **2个节点，不加mirror HA**


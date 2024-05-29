**Rebalance 本质上是一种协议，规定了一个 Consumer Group 下的所有 Consumer 如何达成一致，来分配订阅 Topic 的每个分区。**

- 目的：尽量保持分配策略相对公平，防止**旱的旱死，涝的涝死**

- 劣势：
    1.  Rebalance期间，所有的Consumer都会停止消费消息
    2. Rebalance期间，所有Consumer实例都会参与重分配，可能会导致TCP连接资源的浪费。例如：ConsumerA一直在消费分区1、2，Rebalance后ConsumerA被重分配到分区3、4，那ConsumerA需要重新新建TCP连接而不能复用之前的连接。
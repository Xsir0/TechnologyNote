# kafka
# Kafka
##### Kafka 4个核心API
- Producer API: 用于英语程序将数据流发送到一个或多个Kafka topics
- Consumer API: 用于应用程序订阅一个或多个topics并处理被发送到这些topics中的数据
- Streams API: 允许应用程序作为流处理器，处理来自一个或多个topics的数据并将处理结果发送到一个或多个topics中，有效地将输入流转化为输出流
- Consumer API: 用于构建和运行将Kafka topics和现有应用或数据系统链接的可重用的producers和consumers。例如，链接到关系数据库的连接器可能会捕获到某个表所有的变更。

> Kafka客户端和服务端之间的通信是建立在简单的、高效的、语言无关的TCP协议上的。


对于每一个topic，Kafka会维护一个如下所示的分区日志：

![image](https://kafka.apache.org/0102/images/log_anatomy.png)

- 每个分区是一个有序的，以不可变的记录顺序追加的Commit Log。分区中的每个记录都有一个连续的ID，称为Offset，唯一标识分区内的记录
- Kafka集群使用记录保存时间的配置来保存所有已发布的记录（无论它们是否被消费），例如，配置策略为两天，那么在一条记录发布两天内，这条记录是可以被消费的，之后将被丢弃以腾出空间。Kafka的性能和数据量无关，所以存储长时间的数据并不会成为问题。

- 实际上唯一需要保存的元数据是消费者的消费进度，即消费日志的偏移量（Offset）。这个Offset是由Consumer控制的：通常消费者会在读取记录时以线性方式提升Offset，但是事实上，由于Offset由Consumer控制，因此它可以以任何顺序消费记录。例如一个Consumer可以通过重置Offset来处理过去的数据或者跳过部分数据。

- 分区日志有几个目的。第一，使服务器能承载日志的大小，每个分区的日志必须可以被保存在单个服务器上，但是一个Topic可以拥有多个分区，那么它可以处理任意大小的数据量。第二，它们作为并行度的单位（更多的是这点的考虑）。

##### Kafka as a Messaging System
- Kafka的流模式和传统的消息系统有什么区别？

消息传统上有两种模式：队列和发布-订阅。在队列中，一群Consumer从一个Server读取数据，每条消息被其中一个Consumer读取。在发布-订阅中，消息被广播给所有的Consumer。这两种模式有各自的优缺点。队列模式的优点是你可以在多个消费者实例上分配数据处理，从而允许你对程序进行“伸缩”。确定是队列不是多用户的，一旦消息被一个Consumer读取就不会再给其他Consumer。发布订阅模式允许广播数据到多个Consumer，那么就没办法对单个Consumer进行伸缩。

Kafka的Consumer group包含两个概念。与队列一样，消费组允许通过一些进程来划分处理（每个进程处理一部分）。与发布订阅一样，Kafka允许广播消息到不同的Consumer group。

Kafka模式的优势是每个Topic都拥有队列和发布-订阅两种模式。

`Kafka比传统的消息系统有更强的顺序保证。`

传统的消息系统在服务器上按顺序保存消息，如果多个Consumer从队列中消费消息，服务器按照存储的顺序输出消息。然后服务器虽然按照顺序输出消息，但是消息将被异步的传递给Consumer，所以他们将以不确定的顺序到达Consumer。这意味着在并行消费中将丢失消息顺序。传统消息系统通常采用“唯一消费者”的概念只让一个Consumer进行消费，但这就丢失了并行处理的能力。

Kafka做的更好一些。通过提供分区的概念，Kafka能提供消费集群顺序和负载的平衡。这是通过将分区分配个一个Consumer group中唯一的一个Consumer而实现的，`一个分区只会被一个分组中的一个Consumer进行消费`。通过这么实现，能让一个Consumer消费一个分区并按照顺序处理消息。因为存在多个分区，所有可以在多个Consumer实例上实现负载均衡。
- 注意，一个分组内的Consumer实例数不能超过分区数。

##### Kafka for Stream Processing

- 仅仅是读写和存储流数据是不够的，Kafka的目标是对流失数据的实时处理。

- 在Kafka中，Stream Producer从输入的Topic中读取数据，执行一些操作，生成输出流到输出的Topic中。

 - 例如，零售的应用程序将收到销售和出货的输入流，并输出根据该数据计算的重排序和价格调整后的数据流。

- 可以使用Producer和Consumer实现简单的处理。对于更复杂的转换，Kafka提供的完成的Stream API，允许构建将流中数据聚合或将流连接到一起的应用。

 - 这用于解决以下的一些困难：处理无需的数据，执行有状态的计算等。

- Stream API基于Kafka的核心函数古剑：使用Producer和Consumer API用于输入，使用Kafka作为有状态的存储，使用group机制来实现Stream处理器的容错。

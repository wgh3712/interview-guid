**01 Zookeeper 部分**

- [CAP定理](http://www.ruanyifeng.com/blog/2018/07/cap.html)

  > 含义：一致性、可用性、分区容错性。不可能同时做到；

- ZAB协议

- [leader选举算法和流程](https://www.cnblogs.com/leesf456/p/6107600.html)

**02 Redis 部分**

- Redis的应用场景
- Redis支持的数据类型（必考）
- zset跳表的数据结构（必考）
- Redis的数据过期策略（必考）
- Redis的LRU过期策略的具体实现
- 如何解决Redis缓存雪崩，缓存穿透问题
- Redis的持久化机制（必考）
- Redis的管道pipeline

**03 Mysql 部分**

- 事务的基本要素
- 事务隔离级别
- 如何解决事务的并发问题(脏读，幻读)？
- MVCC多版本并发控制？
- binlog,redolog,undolog都是什么，起什么作用？
- InnoDB的行锁/表锁？
- myisam和innodb的区别，什么时候选择myisam？
- 为什么选择B+树作为索引结构？
- 索引B+树的叶子节点都可以存哪些东西？
- 查询在什么时候不走（预期中的）索引？
- sql如何优化?
- explain是如何解析sql的？
- order by原理

**04 JVM 部分**

- 运行时数据区域（内存模型）
- 垃圾回收机制
- 垃圾回收算法
- Minor GC和Full GC触发条件
- GC中Stop the world
- 各垃圾回收器的特点及区别
- 双亲委派模型
- JDBC和双亲委派模型关系

**05 Java 基础部分**

- HashMap和ConcurrentHashMap区别
- ConcurrentHashMap的数据结构
- 高并发HashMap的环是如何产生的？
- volatile作用
- Atomic类如何保证原子性（CAS操作）
- synchronized和Lock的区别
- 为什么要使用线程池？
- 核心线程池ThreadPoolExecutor的参数
- ThreadPoolExecutor的工作流程
- 如何控制线程池线程的优先级
- 线程之间如何通信
- Boolean占几个字节
- jdk1.8/jdk1.7都分别新增了哪些特性？
- Exception和Error

**06 Spring 部分**

- Spring的IOC/AOP的实现
- 动态代理的实现方式
- Spring如何解决循环依赖（三级缓存）
- Spring的后置处理器
- Spring的@Transactional如何实现的？
- Spring的事务传播级别
- BeanFactory和ApplicationContext的联系和区别

**07 网络编程**

- TCP建立连接和断开连接的过程？
- HTTP协议的交互流程• HTTP和HTTPS的差异，SSL的交互流程？
- TCP的滑动窗口协议有什么用？
- HTTP协议都有哪些方法？
- Socket交互的基本流程？
- 讲讲tcp协议（建连过程，慢启动，滑动窗口，七层模型）？
- webservice协议（wsdl/soap格式，与restt办议的区别）？
- 说说Netty线程模型，什么是零拷贝？
- TCP三次握手、四次挥手？
- DNS解析过程？
- TCP如何保证数据的可靠传输的？

**08 分布式**

- 什么是CAP定理？
- 说说CAP理论和BASE理论？
- 什么是最终一致性？最终一致性实现方式？
- 什么是一致性Hash？
- 讲讲分布式事务？
- 如何实现分布式锁？
- 如何实现分布式 Session?
- 如何保证消息的一致性?
- 负载均衡的理解？
- 正向代理和反向代理？
- CDN实现原理？
- 怎么提升系统的QPS和吞吐？
- Dubbo的底层实现原理和机制？
- 描述一个服务从发布到被消费的详细过程？
- 分布式系统怎么做服务治理？
- 消息中间件如何解决消息丢失问题？
- Dubbo的服务请求失败怎么处理？

**09 其他部分**

- 高并发系统的限流如何实现？
- 高并发秒杀系统的设计
- 负载均衡如何设计？



**面试遇到的问题**：

redis如何解决缓存一致性；
2万的QPS，如何生产短链；



消息队列如何保证消息的有序性；







# java基础

1.   [深入理解hashCode和equals方法](https://www.cnblogs.com/panxuejun/p/5866869.html)

   >- hashCode方法是调用object的hashCode方法计算出hashCode值，然后根据hashCode值计算出对应的位置是否存在元素（hashCode|length-1），如果存在则使用equals()方法进行比较，如果相等则属于同一个元素，如果不相等则属于hash冲突，需要解决hash冲突. 
   >
   >- object的equal相当于==，是比较两个对象的内存地址是否相等；string方法重写了equal方法，比较的是两个对象的值是否相等

2. [java中基本数据类型所占的内存空间](https://www.cnblogs.com/gu-bin/p/9859103.html)

   | boolean | 1  (理论上占用1bit,1/8字节，实际处理按1byte处理) |                |
   | ------- | ------------------------------------------------ | -------------- |
   | byte    | 1                                                | －128～127     |
   | short   | 2                                                | －32768～32767 |
   | char    | 2                                                |                |
   | Int     | 4                                                |                |
   | float   | 4                                                |                |
   | long    | 8                                                |                |
   | double  | 8                                                |                |

3. [jdk8的新特性](http://www.jianshu.com/p/5b800057f2d8)

   > - 函数式接口  (functionalInterface注解  要求只有一个抽象方法）
   > - 接口的默认方法和静态方法
   > - 集合之流式操作
   
4.   [ Atomic类如何保证原子性](https://blog.csdn.net/weixin_44902907/article/details/104745116)

     > 使用cas操作。 java的unsafe类。cas使用版本号来解决A-B-A问题，1A-2B-3A，

# NIO与IO

- [NIO与IO的区别](https://www.cnblogs.com/aspirant/p/8630283.html) ***

  >`区别`
  >
  >1. io面向的是流，nio面向的是缓冲buffer或者说块；所以nio比io快很多；
  >  - java io是面向流，每次从中读取一个或者多个字节，直到读取所有的字节，它没有任何缓冲的地方；
  >  - nio则是面向缓冲区的，它将数据读取到缓存区，可以在缓冲区中前后移动获取到的数据，更灵活；
  >  - nio少了一次从内核空间到用户空间的拷贝，ByteBuffer.allocateDirect分配的内存使用的是本机内存而不是Java堆上的内存，和网络或者磁盘交互都在操作系统的内核空间中发生。
  >2. io是阻塞的，nio是非阻塞的；
  >
  >   - io的各种流是阻塞的。这意味着，一个请求来来后创建一个线程，当线程调用read/write方法时，该线程是被阻塞的，只能处理一个socket请求。直到一些数据被读取完，在此期间该线程不能干任何其他事；
  >   - nio是非阻塞的，一个线程负责接口请求，其它多个线程请求写入一些数据到某个通道，不用等他完全写入，这个线程可以同时干别的事情，所以一个单独的线程现在可以管理多个输入和输出通道（channel）。
  >   - NIO通讯是将整个任务切换成许多小任务，由一个线程负责处理所有io事件，并负责分发。它是利用事件驱动机制，而不是监听机制，事件到的时候再触发。NIO线程之间通过wait，notify等方式通讯。保证了每次上下文切换都有意义，减少无谓的进程切换。 
  >
  >3. io没有选择器，nio是有selector选择器，Selector(多路复用器)用于监听多个通道的事件（比如：连接打开，数据到达）。因此，单个线程可以监听多个数据通道
  >
  >   
  >
  >bio是来一个请求开一个线程，nio是一个线程监听所有的套接字，监测到请求数据后，调用一个线程去处理，对于那些处理事件的线程来说，它多数时间都是在有效的工作，而bio，处理事件的线程亦是监听socket的线程，只要socket fd没准备好，这个线程就只能阻塞。同样1000个链接，使用nio，只需要10个线程就能搞定，使用bio得需要1000个线程

# java泛型

 1. [java泛型总结](https://www.cnblogs.com/coprince/p/8603492.html)

    > 1. 编译之后程序会采取去泛型化的措施。也就是说Java中的泛型，只在编译阶段有效。泛型信息不会进入到运行时阶段；
    >
    > 2. 泛型类、泛型接口、泛型方法（`泛型类，是在实例化类的时候指明泛型的具体类型；泛型方法，是在调用方法的时候指明泛型的具体类型`）
    >
    >     ```java
    >    /**
    >      * 泛型方法的基本介绍
    >      * @param tClass 传入的泛型实参
    >      * @return T 返回值为T类型
    >      * 说明：
    >      *     1）public 与 返回值中间<T非常重要，可以理解为声明此方法为泛型方法。
    >      *     2）只有声明了<T的方法才是泛型方法，泛型类中的使用了泛型的成员方法并不是泛型方法。
    >      *     3）<T表明该方法将使用泛型类型T，此时才可以在方法中使用泛型类型T。
    >      *     4）与泛型类的定义一样，此处T可以随便写为任意标识，常见的如T、E、K、V等形式的参数常用于表示泛型。
    >      */
    >     public <T> T genericMethod(Class<T tClass)throws InstantiationException ,
    >       IllegalAccessException{
    >             T instance = tClass.newInstance();
    >             return instance;
    >     }
    >    ```

#  java反射机制



# 并发多线程

参考：

[多线程常见问题]( http://www.cnblogs.com/xrq730/p/5060921.html)

[java并发编程试题](https://blog.csdn.net/qq_43107323/article/details/104300200)

1. Runnable接口和Callable接口的区别

   > - runnable接口中的run方法的返回值是void
   > - callable接口中的call方法的返回值是泛型的，一般配合future和futureTask对象获取异步操作的结果；  

3. volatile关键字的作用 [volatile关键字深入解析](https://www.cnblogs.com/dolphin0520/p/3920373.html)

   > - 保证了变量在多线程间的可见性，即线程读取到的数据都是最新的数据；
   > - 禁止指令重排序；正常情况下jvm为了获取最佳的性能会进行指令重排序，多线程情况下有可能出现意想不到的问题

4. volatile是如何保证内存可见性的 

   > - 当写一个volatile变量时，JVM会把该线程对应的本地内存中的共享变量刷新到主内存。
   >
   > - 当读一个volatile变量时，JVM会把该线程对应的本地内存置为无效。线程接下来将从主内存中读取共享变量。

4. volatile是如何保证有序性的

   > - 观察他的汇编语言，加入volatile关键字后，会在总线加一个lock锁前缀指令，它确保指令重排序时不会把其后面的指令排到内存屏障之前的位置，也不会把前面的指令排到内存屏障的后面

5. sleep和wait方法的区别

   > - 他们都会使得线程放弃cpu的执行时间 ；
   >
   > - sleep是线程类的方法，wait是object的方法；
   > - sleep可以在任何地方使用，wait只能在同步方法或者同步代码块中使用；
   > - sleep方法不会释放对象的锁，wait方法会释放对象的锁；

5.  ThreadLocal的作用 

   > 它内部维护了一个threadLocalMap对象，key是线程变量，value是保存了每个线程的的本地变量的副本。采用数据隔离、空间换时间的方式保证多线程的安全；

6.  如何在两个线程之间共享数据 

   > 采用wait方法 notify以及notifyAll进行唤醒和等待来实现数据共享

7. 线程池的作用

   > - 避免频繁创建和销毁线程带来的性能损耗；
   > - 提前创建线程，可以降低响应时间；
   > - 更好的规划线程数量，避免线程无节制的创建； 

9. [深入源码分析Java线程池的实现原理](https://www.cnblogs.com/rinack/p/9888717.html)

   >- 线程池底层其实是使用HashSet存储Runnable对象，多余的任务放到阻塞队列

10. [ThreadPoolExecutor线程池的参数](https://www.cnblogs.com/superfj/p/7544971.html)

    > `核心参数`：
    >
    > - corePoolSize：核心线程数
    >
    > - maxPoolSize：最大线程数
    >
    > - keepAliveTime：当线程池中线程数大于核心线程数时，线程的空闲时间如果超过线程存活时间，那么这个线程就会被销毁，直到线程池中的线程数小于等于核心线程数。
    >
    > - Unit：时间单位
    >
    > - workQueue：传输和保存等待执行任务的阻塞队列。
    >
    > - threadFactory：用于创建新线程的线程工厂；
    >
    > - Handler：线程饱和策略 
    >
    > `阻塞队列`: 
    >
    > - ArrayBlockingQueue：有界任务队列，基于数组的有界队列，必须指定大小；
    > - LinkedBlockingQueue，无界的链表的任务队列，创建是可以指定队列的大小；
    > - synchronousQueue：这个队列比较特殊，它不会保存提交的任务，而是将直接新建一个线程来执行新来的任务;
    >
    > `线程池为什么要使用阻塞队列而不使用非阻塞队列？`
    >
    > - 阻塞队列可以保证任务队列中没有任务时阻塞获取任务的线程，使得线程进入wait状态，释放cpu资源。
    > - 当队列中有任务时才唤醒对应线程从队列中取出消息进行执行。使得在线程不至于一直占用cpu资源。
    >
    >  `拒绝策略` 
    >
    > - AbortPolicy：丢弃任务并抛出RejectedExecutionException；
    > - CallerRunsPolicy：只要线程池未关闭，会使用调用线程池的线程来执行任务；
    > - discardOldestPolicy：丢弃队列中最老的一个任务；
    > - DiscardPolicy：丢弃任务，不做任何处理。
    >
    > `线程池流程`：①当线程数小于核心线程池没满的时候会创建线程来执行任务；②当线程数大于核心线程数且阻塞队列没满的时候会放入阻塞队列中；③阻塞队列已满，且最大线程池数，此时会创建线程来执行；
    >
    > ④当达到最大线程数后，会采用拒绝策略来处理任务；
    >
    > `线程池的关闭`: 
    >
    > - shutdown()：不会立即终止线程池，而是要等所有任务缓存队列中的任务都执行完后才终止，但再也不会接受新的任务；
    > - shutdownNow()：立即终止线程池，并尝试打断正在执行的任务，并且清空任务缓存队列，返回尚未执行的任务；
    >
    > `四种常用线程池`: 
    >
    > - **newFixedThreadPool**：固定大小的线程池，可以指定线程池的大小，该线程池corePoolSize和maximumPoolSize相等，阻塞队列使用的是LinkedBlockingQueue，大小为整数最大值，队列会太大，有可能会耗尽系统资源
    > - **newSingleThreadExecutor**：单个线程线程池，只有一个线程的线程池，阻塞队列使用的是LinkedBlockingQueue，大小为整数最大值，队列会太大，有可能会耗尽系统资源。
    > - **newCachedThreadPool**：缓存线程池，缓存的线程默认存活60秒。线程的核心池corePoolSize大小为0，核心池最大为Integer.**MAX_VALUE**，阻塞队列使用的是SynchronousQueue。是一个直接提交的阻塞队列，  他总会迫使线程池增加新的线程去执行新的任务，也会耗尽系统资源；
    > - **newScheduledThreadPool**：周期性的执行任务的线程池；scheduleAtFixedRate:是以固定的频率去执行任务；schedultWithFixedDelay:是以固定的延时去执行任务；

11. [线程和进程的区别](https://www.zhihu.com/question/21535820)

    > - 线程是cpu调度和分派的基本单位，进程是系统进行调度和资源分配的独立单位，进程可以独立运行；
    > - 一个线程只能属于一个进程，而一个进程可以有多个线程，但至少有一个线程；
    > - 资源分配给进程，同一进程的所有线程共享该进程的所有资源。 

12. [Synchronized与ReentrantLock的区别](http://www.cnblogs.com/moonandstar08/p/4973079.html) ***

    > `相同点`
    >
    > - 他们都是可重入锁；
    >
    > `不同点`
    >
    > 1. 实现机制的不同：Synchronized是java的关键字，它是有java虚拟机通过对象头中的mark word字段以及monitor对象来实现的，同步代码块是使用monitorenter和monitorexit指令实现的，同步方法（在这看不出来需要看JVM底层实现）依靠的是方法修饰符上的ACC_SYNCHRONIZED实现。他是悲观锁机制，是独占锁，当发生竞争阻塞的时候，获取不到锁的线程会频繁的上下文切换带来性能损耗；
    >
    >    而reentrantLock是java的类，是java的api，是底层通过调用unsafe.compareAndSetState，他是使用的cas乐观锁的机制，每次不加锁而是假设没有冲突而去完成某项操作，如果因为冲突失败就重试，直到成功为止；
    >
    > 2. lock锁有更多的特性，支持更多的场景：支持公平锁、等待中断锁
    >
    > 3. synchronized使用Object对象本身的wait 、notify、notifyAll调度机制，ReentrantLock里面的Condition应用，能够控制notify哪个线程

13. [synchronized底层实现](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247484838&amp;idx=1&amp;sn=54b33b4c76e136efac09941b2dd346b3&source=41#wechat_redirect)

    > - 对于synchronized同步代码块，会在代码开始和结束的位置有monitorEnter和minitorExit指令，当执行monitorEnter时，线程就必须获取monitor对象的持有权限（monitor对象存在于每个Java对象的对象头中，synchronized 锁便是通过这种方式获取锁的）。
    > - 对于synchronized同步方法，会有ACC_SYNCHRONIZED 标识，表示改方法是同步方法，调用方法前需要获取对象实例的锁

14. Jdk1.6后有的锁优化

    > `锁优化`：引入了偏向锁、轻量级锁、自旋锁10次、自适应自旋锁、锁粗化、锁消除来减少锁操作的开销；
    >
    > `锁状态`  ：无锁状态，偏向锁状态，轻量级锁状态，重量级锁状态
    >
    > `锁优化的意义` ：偏向锁和轻量级锁都是为了减少没有多线程竞争的情况下，重量级锁使用操作系统的互斥量带来的性能损耗。
    >
    > `锁优化的流程`：① 对象的偏向锁会偏向于第一个获取它的线程，接下来如果没有其他线程获取该对象的锁，则持有偏向锁的线程会不执行同步操作；②当有第二个线程获取该锁的时候，偏向锁升级为轻量级锁，轻量级锁使用了cas操作（`主要解决的是绝大部分情况下是不存在竞争的，不需要同步操作`），③轻量级锁不加锁的进行尝试，当失败后不会挂起线程（`因为挂起线程/恢复线程的操作都需要转入内核态中完成（用户态转换到内核态会耗费时间）`）而是在线程周围进行忙循环；当并发冲突比较大的时候会升级为重量级锁；

15. [java锁的详细介绍](https://www.cnblogs.com/jyroy/p/11365935.html)  ???

    > 

16. [CountDownLatch实现原理](https://blog.csdn.net/u014653197/article/details/78217571)

    > `简介` ：CountDownLatch是一个同步工具类，用来协调多个线程之间的同步。这个工具通常用来控制线程等待，它可以让某一个线程等待直到倒计时结束，再开始执行 
    >
    > `原理` ：让需要的暂时阻塞的线程（await），进入一个死循环里面，得到某个条件后再退出循环(count=0)，以此实现阻塞当前线程的效果。

17. [深入理解Semaphore](https://blog.csdn.net/qq_19431333/article/details/70212663) 

    > Semaphore(共享信号量)-允许多个线程同时访问： synchronized 和 ReentrantLock 都是一次只允许一个线程访问某个资源，Semaphore(信号量)可以指定多个线程同时访问某个资源。

18. CyclicBarrier(循环栅栏)  ***

    >  CyclicBarrier 和 CountDownLatch非常类似，它也可以实现线程间的技术等待，但是它的功能比 CountDownLatch 更加复杂和强大。主要应用场景和 CountDownLatch 类似。CyclicBarrier的字面意思是可循环使用（Cyclic）的屏障（Barrier）。CyclicBarrier默认的构造方法是 CyclicBarrier(int parties)，其参数表示屏障拦截的线程数量，每个线程调用await方法告诉 CyclicBarrier 我已经到达了屏障，然后当前线程被阻塞
    >
    >  它要做的事情是，让一组线程到达一个屏障（也可以叫同步点）时被阻塞，直到最后一个线程到达屏障时，屏障才会开门，所有被屏障拦截的线程才会继续干活。

19. [Java并发包基石-AQS详解](https://www.cnblogs.com/chengxiao/archive/2017/07/24/7141160.html)   /[AQS 原理以及 AQS 同步组件总结](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247484832&amp;idx=1&amp;sn=f902febd050eac59d67fc0804d7e1ad5&source=41#wechat_redirect)  ***

    > 1. ` 核心思想`：当被请求的共享资源处于空闲状态，则当前请求资源的线程被标记为有效状态，共享资源被设置为锁定状态。如果被请求的资源被占用，则需要一套线程阻塞等待以及被唤醒时的锁分配的机制，AQS就是使用CLH队列锁来实现的，即将暂时获取不到锁的线程加入到队列中。
    >
    > 2. `资源共享的方式`：独占和共享，其中独占只有一个线程可以执行，如reentrantLock，又分为公平和非公平的；共享是指多个线程可以同时执行，如countDownLatch/ Semaphore
    >
    > 3. `AQS底层使用了模板方法模式`：使用的时候需要继承AQS类，重写如下方法
    >
    >    ```
    >    isHeldExclusively()//该线程是否正在独占资源。只有用到condition才需要去实现它。
    >    tryAcquire(int)//独占方式。尝试获取资源，成功则返回true，失败则返回false。
    >    tryRelease(int)//独占方式。尝试释放资源，成功则返回true，失败则返回false。
    >    tryAcquireShared(int)//共享方式。尝试获取资源。负数表示失败；0表示成功，但没有剩余可用资源；正数表示成功，且有剩余资源。
    >    tryReleaseShared(int)//共享方式。尝试释放资源，成功则返回true，失败则返回false
    >    ```

20. synchronized和volatile的区别

    > 1. 粒度不同，前者锁对象和类，后者针对变量；
    > 2. syn保证三大特性，volatile不保证原子性；
    > 3. syn阻塞，volatile线程不阻塞；
    > 4. syn编译器优化，volatile不优化；

21. 悲观锁和乐观锁

    > - 乐观锁是假设并发冲突不会发生，总是不加锁的执行操作，如果失败，则会进行重试；
    > - 悲观锁是假设冲突会发生，执行操作的时候就加一个独占锁；

22. cas是什么

    > cas就是comare and swap，就是内存值V，旧值A，要修改的值b，只有当预期值A与内存的值V相等时才执行设置值为b，并且返回成功，否则返回失败；一般是配合volatile关键字使用，才可以保证拿到的变量主内存中的值，修改后可以将值设置到主内存中去；

23. java内存模型  ***

    > 1. java内存模型分为主内存和工作内存，共享变量保存在主内存中，每一个线程需要修改和读取共享变量的时候都要从主内存中copy一份到自己的工作内存中，修改完后会写到主内存中去；
    >
    > 2. 定义了volatile的使用规则，保证每个线程读取volatile修饰的字段，都可以读取到最新的值，写的值都可以写到主内存中去；
    >
    > 3. 定义了原子操作，用于操作主内存和工作内存中的变量；
    >
    >    ```
    >    lock（锁定主内存）
    >    unlock（解锁主内存）
    >    read（读取主内存，为load准备）
    >    load（载入主内存至工作内存）
    >    use（执行引擎使用工作内存）
    >    assign（接受执行引擎计算后的值赋值给工作内存）
    >    store（存储工作内存至主内存，为write准备）
    >    write（把工作内存写入主内存）
    >    ```
    >
    > 4. 定义了happen-before，即先行发生规则，一个unlock操作一定先行发生于对后面的同一个锁进行lock操作；同一个线程，前面的操作一定先行执行与后面的操作；
    >
    > 5. 指令重排序，只要和源代码产生的结果一样，编译器会进行操作的重排序，提升计算机性能；

24. Happens-before 关系

    > 如果线程 A 与线程 B 满足 happens-before 关系，则线程 A 执行动作的结果对于线程 B 是可见的
    >
    > - 程序次序法则：一个线程内，按照代码顺序，书写在前面的操作先行发生于书写在后面的操作
    > - 监视器锁法则：一个unLock操作先行发生于后面对同一个锁的lock操作
    > - Volatile 变量法则：对一个Volatile变量的写操作先行发生于后面对这个变量的读操作
    > - 传递性：如果 A happens-before 于 B，且 B happens-before C，则 A happens-before C。

25. Thread.sleep(0)的作用是什么

    > 由于java使用抢占式调度算法，而sleep操作可以放弃cpu的执行时间，这样可以操作系统重新进行一次操作系统重新分配时间片的操作；  

# java的集合数据结构

# List相关

1. [arrayList和vector的区别](https://blog.csdn.net/qq_37113604/article/details/80836025?utm_medium=distribute.pc_relevant.none-task-blog-baidujs-1)

   > - arrayList是数组来实现的，初始容量10，Arrays.copyOf 扩容为1.5倍；线程不安全
   >
   > - vector也是数组来实现的，初始容量10，默认扩容为2倍，可以制动扩容因子；synchronized修饰线程安全；

2. [arrayList](https://blog.csdn.net/ywlmsm1224811/article/details/91388048)

   > arrayList继承了abstractList，最上层是collection接口，RandmoAccess接口随机访问表示；
   >
   > 多线程选择vector和copyOnWriteArrayList

# hashMap相关

1. 如何解决hash冲突

   > 1. 开放地址法：
   >
   > 优点：开放寻址法不像链表法，需要拉很多链表，他们需要根据指针寻址，对cpu不友好。散列表中的数据都存储在数组中，可以有效地利用CPU缓存加快查询速度；
   >
   > 缺点：用开放寻址法解决冲突的散列表，删除数据的时候比较麻烦，需要特殊标记已经删除掉的数据。而且，在开放寻址法中，所有的数据都存储在一个数组中，比起链表法来说，冲突的代价更高。
   >
   > ​       当数据量比较小、装载因子小的时候，适合采用开放寻址法。这也是Java中的ThreadLocalMap使用开放寻址法解决散列冲突的原因。
   >
   > 2.链表法：
   >
   > ​     优点：首先，链表法对内存的利用率比开放寻址法要高。因为链表结点可以在需要的时候再创建，并不需要像开放寻址法那样事先申请好。
   >
   > ​    其次  对装载因子的容忍度高，即使装很多元素只是查找效率下降而已；
   >
   > ​    最后  链表法比较灵活，可以修改实现改为红黑树；
   >
   > ​    缺点：如果存储的小对象，那么指针消耗也是很大一部分
   >
   > ​    基于链表的散列冲突处理方法比较适合存储大对象、大数据量的散列表，而且，比起开放寻址法，它更加灵活，支持更多的优化策略，比如用红黑树代替链表。

2. [为什么hash表的容量一定要是2的整数倍](https://www.cnblogs.com/peizhe123/p/5790252.html)

   > 为了使不同 hash 值发生碰撞的概率更小，尽可能促使元素在哈希表中均匀地散列。
   >
   > - 2的整数倍减1后，换成二进制后，最后一位肯定是1，这样与hashCode与操作，有可能是奇偶，否则只能是偶数，会浪费一般空间而且不能保证散列均匀；
   >
   > capacity 为 2 的整数次幂的话，为偶数，这样 capacity-1 为奇数，奇数的最后一位是 1，这样便保证了 h&(capacity-1) 的最后一位可能为 0，也可能为 1（这取决于h的值），即与后的结果可能为偶数，也可能为奇数，这样便可以保证散列的均匀性；
   >
   > 而如果 capacity 为奇数的话，很明显 capacity-1 为偶数，它的最后一位是 0，这样 h&(capacity-1) 的最后一位肯定为 0，即只能为偶数，这样任何 hash 值都只会被散列到数组的偶数下标位置上，这便浪费了近一半的空间。

   > - 而与操作是使用取余替代取模，提升计算效率；
   >
   >    首先，capacity 为 2的整数次幂的话，长度减一后相当于低位的掩码，计算桶的位置 h&(length-1) 就相当于对 length 取模，提升了计算效率；
   
3. [hashmap多线程操作导致死循环](https://coolshell.cn/articles/9606.html) 

   [hashmap死循环](https://blog.csdn.net/xuefeng0707/article/details/40797085)

   > hashmap在多线程的情况下进行rehash操作会导致死循环；

4. rehash算法

   > ![img](https://pic2.zhimg.com/80/a285d9b2da279a18b052fe5eed69afe9_720w.png)
   >
   > - rehash的算法中，扩容为2倍后，重新计算索引，index = 原位置+oldcap或者为原index；
   >
   > - 只需要看看原来的hash值新增的那个bit是1还是0就好了，是0的话索引没变，是1的话索引变成“原索引+oldCap”，可以看看下图为16扩充为32的resize示意图：
   >
   > 

5. hashmap的hash算法  ***

   >
   >
   >![img](https://pic2.zhimg.com/80/8e8203c1b51be6446cda4026eaaccf19_720w.png)
   >
   >int hash(Object key) {
   >int h = key.hashCode()；
   >return (h ^ (h >>> 16)) & (capitity -1); //capicity 表示散列表的大小
   >}
   >
   >先补充下老师使用的这段代码的一些问题：在JDK HashMap源码中，是分两步走的：
   >
   >1. hash值的计算，源码如下：
   >    static final int hash(Object key) {
   >       int hash;
   >       return key == null ? 0 : (hash = key.hashCode()) ^ hash >>> 16;
   >     }
   >2. 在插入或查找的时候，计算Key被映射到桶的位置：
   >    int index = hash(key) & (capacity - 1)

   >- JDK HashMap中hash函数的设计，确实很巧妙：
   >
   >首先hashcode本身是个32位整型值，获取对象的hashcode以后，先进行移位运算，然后再和自己做异或运算，即：hashcode ^ (hashcode >>> 16)，这一步甚是巧妙，是`将高16位移到低16位，这样计算出来的整型值将“具有”高位和低位的性质`
   >
   >最后，用hash表当前的容量减去一，再和刚刚计算出来的整型值做位与运算。进行位与运算，很好理解，是为了计算出数组中的位置。但这里有个问题：
   >为什么要用容量减去一？
   >因为 A % B = A & (B - 1)，所以，(h ^ (h >>> 16)) & (capitity -1) = (h ^ (h >>> 16)) % capitity，可以看出这里本质上是使用了「除留余数法」
   >
   >综上，可以看出，hashcode的随机性，加上移位异或算法，得到一个非常随机的hash值，再通过「除留余数法」，得到index，

6. HashMap如何避免低效地扩容  ***

   >   大部分情况下，动态扩容的散列表插入一个数据都很快，但是在特殊情况下，当装载因子已经到达阈值，需要先进行扩容，再插入数据。这个时候，插入数据就会变得很慢，甚至会无法接受。我举一个极端的例子，如果散列表当前大小为1GB，要想扩容为原来的两倍大小，那就需要对1GB的数据重新计算哈希值，并且从原来的散列表搬移到新的散列表，听起来就很耗时，是不是？
   >
   > ​        如果我们的业务代码直接服务于用户，尽管大部分情况下，插入一个数据的操作都很快，但是，极个别非常慢的插入操作，也会让用户崩溃。这个时候，“一次性”扩容的机制就不合适了。
   >
   > ​        为了解决一次性扩容耗时过多的情况，我们可以将扩容操作穿插在插入操作的过程中，分批完成。当装载因子触达阈值之后，我们只申请新空间，但并不将老的数据搬移到新散列表中。
   >
   > ​        当有新数据要插入时，我们将新数据插入新散列表中，并且从老的散列表中拿出一个数据放入到新散列表。每次插入一个数据到散列表，我们都重复上面的过程。经过多次插入操作之后，老的散列表中的数据就一点一点全部搬移到新散列表中了。这样没有了集中的一次性数据搬移，插入操作就都变得很快了。
   >
   > ​    对于查询操作，为了兼容了新、老散列表中的数据，我们先从新散列表中查找，如果没有找到，再去老的散列表中查找。

7. [hashMap的源码解析1.8](https://zhuanlan.zhihu.com/p/21673805)

   [hashMap的源码解析1.7](https://www.cnblogs.com/peizhe123/p/5790252.html)

   > `1.8的put流程`：
   >
   > ①.判断键值对数组table[i]是否为空或为null，否则执行resize()进行扩容；
   >
   > ②.根据键值key计算hash值得到插入的数组索引i，如果table[i]==null，直接新建节点添加，转向⑥，如果table[i]不为空，转向③；
   >
   > ③.判断table[i]的首个元素是否和key一样，如果相同直接覆盖value，否则转向④，这里的相同指的是hashCode以及equals；
   >
   > ④.判断table[i] 是否为treeNode，即table[i] 是否是红黑树，如果是红黑树，则直接在树中插入键值对，否则转向⑤；
   >
   > ⑤.遍历table[i]，判断链表长度是否大于8，大于8的话把链表转换为红黑树，在红黑树中执行插入操作，否则进行链表的插入操作；遍历过程中若发现key已经存在直接覆盖value即可；
   >
   > ⑥.插入成功后，判断实际存在的键值对数量size是否超多了最大容量threshold，如果超过，进行扩容。

8. 负载因子的作用

   >  负载因子是hash冲突和内存空间利用率的一种折中。
   >
   >  若负载因子越大，装载的元素越多，空间利用率高了，但是冲突变大，链表变长，查找效率变低；
   >
   >  若负载因子越小，状态的元素变少，空间表少了，冲突变小，查找起来更快；

9. hashMap的modCount用来的作用

   > modCount字段是用来记录hashmap内部结构发生变化的次数，主要用于迭代的快速失败。例如put新键值对，如果某个key对应的value被覆盖不属于结构变化。遍历过程中改变hashMap的内部机构则会出现ConcurrentModificationException。

10. 多线程操作hashMap会出现什么问题

    > - 在rehash时会出现死循环；rehash会重新将原数组的内容重新hash到新的扩容数组中，在多线程的环境下，存在同时其他的元素也在进行put操作，如果hash值相同，可能出现同时在同一数组下用链表表示，造成闭环，导致在get时会出现死循环
    > - 在遍历的时候修改hashmap的结构，会出现concurrentModifyException，fail-fast机制

11. [linkHashMap](https://www.imooc.com/article/22931)

    > - linkHashMap是在 HashMap 基础上，通过维护一条双向链表，解决了 HashMap 不能随时保持遍历顺序和插入顺序一致的问题。
    >
    > - LinkedHashMap 对访问顺序也提供了相关支持。在一些场景下，该特性很有用，比如缓存。
    >
    > - 添加元素是将新元素放到双向链表的尾部。
    > - 实现访问控制，就是在get元素后，将节点放到双向链表的尾部；移除最近最少访问的元素在头部；需要重写removeEldestEntry方法，订制删除策略

12. [fail-fast 机制](https://baijiahao.baidu.com/s?id=1638201147057831295&wfr=spider&for=pc)

    > - Fail-fast机制是指在系统设计中，快速失效系统一种可以立即报告任何可能表明故障的情况的系统。快速失效系统通常设计用于停止正常操作，而不是试图继续可能存在缺陷的过程。
    >
    > - arrayList和hashmap就使用modCount字段来记录表机构修改的次数，来和遍历过程中获取的次数进行对比，如果不一致，则fail-fast;

13. concurrentHashMap

    [concurrentHashMap]( https://www.ibm.com/developerworks/cn/java/java-lo-concurrenthashmap/index.html)

    [concurrentHashMap-1.8](https://www.cnblogs.com/yangming1996/p/8031199.html)

    > `jdk1.7与1.8的实现机制`
    >
    > - Jdk1.7采用的分段锁技术，整个hash表被分成多个段，每个段对应一个segment锁。段与段之间的可以并发访问，同一个段之间并发访问需要获取锁；
    > - Jdk1.8取消了segment分段锁机制，采用cas+synchronized控制并发，使用数组加链表+红黑树取代了数组+链表。
    >
    > `concurrentHashMap 1.8`:
    >
    > `sizeCtl 属性`：代表是初始化哈希表，还是扩容 rehash 的过程
    >
    > - 0：默认值
    > - -1：代表哈希表正在进行初始化
    > - 大于0：相当于 HashMap 中的 threshold，表示阈值
    > - 小于-1：代表有多个线程正在进行扩容
    >
    > `putval方法`
    >
    > 1. 如果没有初始化就先调用initTable（）方法来进行初始化过程
    >
    > 2. 如果没有hash冲突就直接CAS插入
    >
    > 3. 如果还在进行扩容操作就先进行扩容
    >
    > 4. 如果存在hash冲突，就加锁来保证线程安全，这里有两种情况，一种是链表形式就直接遍历到尾端插入，一种是红黑树就按照红黑树结构插入，
    >
    > 5. 最后一个如果该链表的数量大于阈值8，就要先转换成黑红树的结构，break再一次进入循环
    >
    > 6. 如果添加成功就调用addCount（）方法统计size，并且检查是否需要扩容
    >
    >    
    >
    > - 放置元素的时候，如果对应的位置为空，则以cas的方式在对应的位置添加节点；
    > - hash表只允许一个线程进行初始化，判断sizeCtl属性，来判断U.compareAndSwapInt初始化；
    > - 扩容的时候需要会使用多线程扩容；helpTransfer（）方法是调用多个工作线程一起帮助进行扩容
    > - volatile`类型的变量`baseCount记录元素的个数，通过cas的方式修改baseCount
    >
    > 
    >
    > `concurrentHashMap 1.7`:
    >
    > ```java
    > static final class Segment<K,V> extends ReentrantLock implements Serializable {
    >         transient volatile HashEntry<K,V>[] table;
    >         transient int count;
    >         transient int modCount;
    >         transient int threshold;
    >         final float loadFactor;
    > ```
    >
    > -	Segment的put方法：需要通过tryLock获取到该段的锁，然后才可以执行put操作；
    > -	size方法：先采用不加锁的方式，连续计算多个segment元素的个数，最多计算3次：
    >    1、如果前后两次计算结果相同，则说明计算出来的元素个数是准确的；
    >    2、如果前后两次计算结果都不同，则给每个`Segment`进行加锁，再计算一次元素的个数；
    >
    > `concurrentHashMap不允许空key和空value；hashMap允许一个空key，多个空value`

14. [一致性hash算法](https://www.jianshu.com/p/e968c081f563)

    > `意义`：
    >
    > 普通的hash算法，可以使每台机器固定处理一部分用户请求，起到负载均衡的作用；但当一些机器失效的时候，用户id与服务器的映射关系会大量失效；此时一致性hash算法诞生；
    >
    > `总结`：
    >
    > 环状、可以使用虚拟节点来减少节点失效的影响。
    >
    > 1、2、3、4、5、6、7、8、9
    >
    > A：1、4、7；B：2、5、8；C：3、6、9

    

# 队列

1. [java的队列-queue](https://blog.csdn.net/qq_33524158/article/details/78578370)

   > `ConcurrentLinkedQueue`：是一个适用于高并发场景下的队列，通过无锁的方式，实现了高并发状态下的高性能。头是最先加入的，尾是最近加入的，该队列不允许null元素。
   >
   > `blockingQueue`:
   >
   > - ArrayBlockingQueue是基于`数组`的阻塞队列，内部维护一个`定长`数组缓冲队列，`有界`队列，内部`没有实现读写分离`，意味着生产和消费不能并行；
   > - LinkedBlockingQueue：基于链表的阻塞队列，内部也维护着缓存队列，无界的，内部实现读写分离，支持并发；
   > - SynchronousQueue：一种没有缓冲的队列，生产者产生的数据直接会被消费者获取并消费。
   > - PriorityBlockingQueue：基于优先级的阻塞队列（优先级的判断通过构造函数传入的Compator对象来决定，也就是说传入队列的对象必须实现Comparable接口），在实现PriorityBlockingQueue时，内部控制线程同步的锁采用的是公平锁，他也是一个无界的队列；
   > - DelayQueue：带有延迟时间的Queue，其中的元素只有当其指定的延迟时间到了，才能够从队列中获取到该元素。
   >
   > `Deque 双端队列`:
   >
   > -  LinkedBlockingDeque是一个线程安全的双端队列实现，可以说他是最为复杂的一种队列，在内部实现维护了前端和后端节点，但是其没有实现读写分离，因此同一时间只能有一个线程对其讲行操作。

# JVM

1. JVM运行内存的分类  [深入java虚拟机总结](https://www.cnblogs.com/wangzhongqiu/p/8908266.html)

   > - 程序计数器：存放的是虚拟机正在执行的字节码指令，可以看成是当前线程所执行的字节码行号，线程私有；
   >
   > - java虚拟机栈：线程私有，每个方法执行的时候都会创建一个栈帧，方法执行过程对应着栈帧入栈和出栈的过程；存储局部变量表、操作数栈、动态链接、方法返回值等；包含基本数据类型和对象的引用；
   > - 本地方法栈：和虚拟机栈一样，不过是为虚拟机的native方法服务；
   > - java堆：是线程共享的，是垃圾回收的主要区域；主要包括所有的对象实例、包括数组；
   > - 方法区：线程共享，虚拟机加载的类信息、常量、静态变量、也就是老年代；回收目标主要是常量池的回收和类型的卸载。jdk1.8使用metaSpace来代替永久代方法区；
   > - 运行时常量池：是方法区的一部分，主要包括常量池，比如integer的-127-128、string的intern()方法返回的字符串对象等；
   > - 直接内存：也叫堆外内存，不是jvm的运行区域的一部分，是java1.4加入的NIO可以使用native方法直接分配堆外内存，Java堆中的DirectByteBuffer对象作为这块内存的引用进行操作。

2. HotSpot虚拟机

   - 对象的创建

   > - 为对象分配内存，如果是规整的采用指针碰撞的方式；不规整的采用空闲列表，内存是否规则看是否代用压缩的功能；
   >
   > - serial、parNew带有压缩功能使用的是指针碰撞，cms使用的是空闲列表；

   - 对象涉及到分配内存和指针指向两个操作，不是原子性的，不是线程安全的。

   > 1. 使用cas加上失败重试来保证原子性；
   > 2. 使用TLAB（Thread Local Allocation Buffer）策略，预先为每个线程分配一块内存，那个线程需要就各自分配，只有用完的时候才需要锁定同步；是否使用TLAB 需要配置-XX:+/- UseTLAB；

   - 设置对象头

   > 内存分配完后需要设置对象头，包括对象所属的实例，对象的hash码，对象的分代年龄、对象的元数据信息，锁状态标志、偏向线程ID、偏向时间戳；

   - 对象的访问定位

   > 1. 使用reference句柄，最大好处是当对象修改时reference本身不需要修改；
   > 2. 使用直接指针，节省了一次指针的开销，访问速度快；

3. 四种引用

   > 强引用：java虚拟机不会回收；
   > 软引用：如果内存空间不足了，就会回收这些对象的内存；
   > 弱引用：与软引用相比弱引用的对象拥有更短暂的生命周期，一旦发现了只具有弱引用的对象，不管当前内存空间足够与否，都会回收它的内存；
   > 虚引用：主要用来跟踪对象被垃圾回收器回收的活动，被回收时会收到一个系统通知；

   4. GC标记对象死活

   > - 引用计数法：给对象添加一个引用计数器，被引用就加一，引用失效就减一；判断效率高，但无法解决循环引用的问题；
   > - 可达性分析算法：以一个GCRoot对象作为起点，从这个节点向下搜索，搜索走过的路径称为引用链，当一个对象没有与引用链中任何对象相连，则对象就被标记位可回收；

   5. GC Roots都有哪些

   > - 虚拟机栈中的引用的对象；
   >
   > - 本地方法栈中JNI（即一般说的Native方法）引用的对象；
   >
   > - 方法区中静态属性引用的对象，常量引用的对象

   6. 对象被回收的过程

   > -  使用GCRoot标记可回收后判断是否需要执行finalize()方法（重写了或者手动调用了finalize()方法就需要执行）；
   >
   > - 如果需要执行，则放入F-queue队列中，虚拟机会在稍后执行，如果在执行finalize方法时与GCRoot产生引用链，则可以逃脱被回收的命运；

   7. GC垃圾回收算法

   > - 标记-清除算法：标记出没有用的对象，然后进行清除；缺点标记和清除的算法都不高，且会产生内存碎片；
   > - 复制算法：容量等大分为两份，一份满了，将存活的复制到另一份中；缺点浪费空间；
   > - 标记-整理：标记出存活的对象，让存活的对象移动到一端，直接清除端以外的对象；优点是解决了标记清除导致的内存碎片问题；
   > - 分代回收：根据对象的存活时间分为年轻代和老年代，年轻代使用复制算法，老年代使用标记整理算法，cms采用标记清除算法；

   8. 内存分配和回收策略

   > - 结构： 年轻代（1/3）生命周期短，8:1:1 eden:survival ;老年代 (2/3):生命周期长
   > - 小对象先在年轻代区分配；
   > - 大对象直接进入老年代；
   > - 长期存活的对象，指多次在年轻代中复制达到阈值，进入老年代；
   > - 动态对象年龄判断。如果在Survival空间中相同年龄所有对象的大小总和超过了Survival空间的一半，年龄大于等于这个年龄的对象都会被晋升到老年代。无需等待年龄超过MaxTenuringThreShold指定的年龄；

   9. [Full GC 和 Minor GC](https://juejin.im/post/5b8d2a5551882542ba1ddcf8)

   > - yongGC只回收年轻代，
   > - oldGC只收集老年代（CMS才有的称呼）；
   > - fullGC收集整个堆，包括年轻代、老年代以及永久代（1.8后由metaspace取代了永久代）

   10. Full GC的触发条件,不同垃圾回收期的触发条件不同 ***

   > - serial GC收集器下：
   >   1. 当触发一次yongGC前，如果发现yongGC的平均晋升大小比老年代的剩余空间大，则会转yongGC为fullGC；
   >   2. 如果永久代没有足够的分配空间，则需要出发一次fullGC；
   >   3. 使用system.gc()方法，默认是出发full gc； 

   > - Parallel Scavenge 收集器下默认出发fullGC前需要先进行一次yongGC，并且两次GC之间能让应用程序稍微运行一小下，以期降低 full GC的暂停时间；

   > - CMS收集器下，先检查old gen的大小，达到触发比例才会启动old gc；

   11. Survivor区对象晋升为老年代对象的条件

   > 1. Survivor区中的对象被来回复制的次数会被记录下来。如果一个对象被复制的次数为 15 (对应虚拟机参数 -XX:+MaxTenuringThreshold),那么该对象将被晋升为至老年代;
   > 2. 动态对象年龄判断。如果在Survival空间中相同年龄所有对象的大小总和超过了Survival空间的一半，年龄大于等于这个年龄的对象都会被晋升到老年代。无需等待年龄超过MaxTenuringThreShold指定的年龄；
   12. 垃圾收集器 ***

   > Serial 收集器是针对新生代的收集器，单线程收集器，采用的是复制算法；
   > Parallel New（并行）收集器，Serial的多线程版本 新生代采用复制算法，cms的搭配使用；
   > Parallel Scavenge（并行）收集器，针对新生代，采用复制收集算法，关注的是吞吐量；
   > Serial Old（串行）收集器，老年代采用标记清理
   > Parallel Old（并行）收集器，针对老年代，标记整理
   > CMS收集器，基于标记清理，老年代收集器，注重的是最短停顿时间；
   > G1收集器(JDK)：整体上是基于标记-整理，分代收集
   > 综上：新生代基本采用复制算法，老年代采用标记整理算法。cms采用标记清除

   13. CMS 收集器与G1收集器 ***

   > CMS垃圾收集器
   >
   > - 特点：cms，最短停顿时间为目标，基于标记-清除算法；
   > - 流程：初始标记、并发标记、重新标记、并发清除；
   > - 各个阶段的作用：初始标记是标记GCRoot直连的；
   >    并发标记是通过GCRoot往下寻找；
   >   重新标记为了修正并发标记期间程序运行导致的变动的对象，时间比初始标记长，比并发标记短；
   >   耗时最长的并发标记和并发清除不会停顿，用户线程和处理线程一起工作；
   > - 缺点：
   >   1. 垃圾回收时占用线程，导致系统变慢，吞吐量降低；
   >   2. 使用标记-清除算法，容易产生内存碎片；需要开启碎片整理功能，多少次fullgc后开启一次带压缩的fullGC,使用-XX:CMSFullGCsBeforeCompaction
   >   3. 无法处理浮动垃圾，并发操作期间需要预留给用户的线程的内存，否则会出现 Concurrent Mode Failure 错误，需要使用 serial old，进行垃圾回收，导致停顿时间边长；

   > G1收集器
   >
   > - 特点：包括新生代和老年代的垃圾回收；并行并发，分代收集，标记-整理，可预测的停顿；
   > - 流程：
   >   初始标记：标记GC Roots能够直接关联到的对象，这阶段需要停顿线程，时间很短
   >   并发标记：进行可达性分析，这阶段耗时较长，可与用户程序并发执行
   >   最终标记：修正发生变化的记录，需要停顿线程，但是可并行执行
   >   筛选回收：对各个Region的回收价值和成本进行排序，根据用户所期望的停顿时间来执行回收计划

   14. 虚拟机性能监控工具 ***

       >1. jps，直接带有权限的hotspot虚拟机进程；
       >
       >2. jstat -gcutil proessId interval count ,可以查看堆的各个区的使用情况，垃圾回收次数和时间等的统计；
       >3. jmap jmap -dump:live,format=b,file=dump.hprof 24971,查看内存的dump文件
       >4. jinfo -flag +PrintGCDetails 105704 查看和修改JVM运行参数
       >5. jstack  jstack pid - Java堆栈跟踪工具 。dead lock问题，占用cpu时间最多的线程，频繁GC
       >6. jconsole 可视化工具，内存，线程，垃圾回收，配合各种插件使用；
       >7. jvisual
       >8. [mat eclipse](https://blog.csdn.net/qeqeqe236/article/details/43577857) 开源的内存分析工具，将dump的文件导入后。提供可以查看对象的引用关系、最占内存的对象、疑似内存泄漏点等功能；

   15. [虚拟机参数](https://www.cnblogs.com/redcreen/archive/2011/05/04/2037057.html)

   ```
   128G内存，40核cpu
   
   CMS+ParNew
   -Xms8G
   -Xmx8G
   -Xmn3G
   -Xss512k
   -XX:MetaspaceSize=512m
   -XX:MaxMetaspaceSize=512m
   -XX:+PrintGCDetails
   -XX:+UseParNewGC
   -XX:ParallelGCThreads=6
   -XX:+UseConcMarkSweepGC
   -XX:+CMSParallelRemarkEnabled
   -XX:SurvivorRatio=8
   -XX:NewRatio=4      //新生代：老年代=1：4
   -XX:CMSInitiatingOccupancyFraction=70  //老年代垃圾占比达到这个阈值开始CMS收集，设置过高容易导致并发收集失败，会出现SerialOld收集的情况
   -XX:CMSFullGCsBeforeCompaction=5
   -XX:+UseCMSCompactAtFullCollection
   -XX:+HeapDumpOnOutOfMemoryError
   
   ```

   16. [java类加载过程](https://blog.csdn.net/shuangyue/article/details/9262791) ***

   > 类加载被分为加载、连接、初始化过程；连接又细分为验证、准备和解析；
   >
   > 1. 装载：jvm将字节码文件以二进制的方式读入到内存中，转化为运行时数据结构；
   > 2. 连接：主要做加载完的准备工作，验证字节码是否符合规范；为静态变量分配内存，分配初始值；解析类、字段、接口，将符号引用转换为直接引用；
   > 3. 初始化：new实例或者读取设置类的静态变量；反射方式执行以上行为；初始化子类的时候触发父类初始化；作为程序入口的主类；
   

   17. 两种主动加载方式

   >class.forName()静态方法；
   >classLoader.loadClass()方法；

   18. 双亲委派模型

       > - 被不同类加载器加载的同名类，也认为是不同的类。
       >
       > - 双亲委派模型。分为两种类加载器： 1 是启动类加载器 ，是虚拟机自身的一部分；2 是所有的其他类加载器，这些类加载器都由java语言实现。独立于虚拟机外部，全部继承自java.lang.ClassLoader抽象类。类加载器具体层次关系：启动类加载器->扩展类加载器->系统类加载器->自定义类加载器。每一个类的加载，会优先由父加载器来加载。这种方式就称为双亲委派，双亲委派保证了java基本类的不会被破坏和替代

       

# 设计模式 ?

- 单例模式（2种模式以及调优）
- 工厂模式 （静态工厂模式、工厂方法模式、抽象工厂模式）
- 策略模式
- 代理模式
- 模板方法模式
- 适配器模式
- [动态代理模式](https://www.cnblogs.com/gonjan-blog/p/6685611.html)
- [23种设计模式](https://blog.csdn.net/jason0539/article/details/44956775)

# mybatis 

1. [常见问题](http://www.cnblogs.com/huajiezh/p/6415388.html)

2. #{}和${}的区别是什么？

   > ${}是properties文件中变量的占位符，可以用于java中属性注入和sql内部，属于静态文本替换；
   >
   > #{}是sql参数占位符，mybatis会将sql中#{}替换为？，在执行前使用prepareStatement设置参数值；

3. mybatis的xml中常用的标签

   > <resultMap>、<parameterMap>、<sql>、<include> trim|where|set|foreach|if|choose|when|otherwise|bind

4. 简述Mybatis的插件运行原理，以及如何编写一个插件。

   > Mybatis仅可以编写针对ParameterHandler、ResultSetHandler、StatementHandler、Executor这4种接口的插件，Mybatis使用JDK的动态代理，为需要拦截的接口生成代理对象以实现接口方法拦截功能，每当执行这4种接口对象的方法时，就会进入拦截方法，具体就是InvocationHandler的invoke()方法，当然，只会拦截那些你指定需要拦截的方法。
   >
   > 实现Mybatis的Interceptor接口并复写intercept()方法，然后在给插件编写注解，指定要拦截哪一个接口的哪些方法即可，记住，别忘了在配置文件中配置你编写的插件。

# springboot  

1. [spring常用注解](https://blog.csdn.net/lafengwnagzi/article/details/53034369)

   > - @RestController注解代替 @Controller和@responseBody注解；
   >
   > - @EnableAutoConfiguration注解，这个注解告诉Spring Boot根据添加的jar依赖猜测你想如何配置Spring。由于 spring-boot-starter-web 添加了Tomcat和Spring MVC，所以auto-configuration将假定你正在开发一个web应用并相应地对Spring进行设置
   >
   > - @Configuration：Spring Boot提倡基于Java的配置，@Import 注解可以用来导入其他配置类。另外，你也可以使用 @ComponentScan 注解自动收集所有的Spring组件。
   >
   > - @SpringBootApplication 等价于@Configuration @EnableAutoConfiguration 和 @ComponentScan；
   >
   > - @ConfigurationProperties(prefix="connection") 注入熟悉文件的前缀约束；
   >
   > - @ResponseBody：表示该方法的返回结果直接写入HTTP response body中，一般在异步获取数据时使用，在使用@RequestMapping后，返回值通常解析为跳转路径，加上@responsebody后返回结果不会被解析为跳转路径，而是直接写入HTTP response body中。比如异步获取json数据，加上@responsebody后，会直接返回json数据。
   >
   > - @AutoWired，byType方式。把配置好的Bean拿来用，完成属性、方法的组装
   >
   > - @RequestParam：用在方法的参数前面。
   >
   >   > ```java
   >   > @RequestParam String a =request.getParameter("a")。
   >   > ```
   >
   > - @PathVariable：路径变量
   >
   >   ```java
   >   @RequestMapping("user/get/mac/{macAddress}")
   >   public String getByMacAddress(@PathVariable String macAddress)
   >   ```
   >
   > - @ControllerAdvice：全局异常处理。@ExceptionHandler（Exception.class）
   >
   >   ```java
   >   
   >   /**
   >    * 全局异常处理
   >    */
   >   @ControllerAdvice
   >   class GlobalDefaultExceptionHandler {
   >       public static final String DEFAULT_ERROR_VIEW = "error";
   >    
   >       @ExceptionHandler({TypeMismatchException.class,NumberFormatException.class})
   >       public ModelAndView formatErrorHandler(HttpServletRequest req, Exception e) throws Exception {
   >           ModelAndView mav = new ModelAndView();
   >           mav.addObject("error","参数类型错误");
   >           mav.addObject("exception", e);
   >           mav.addObject("url", RequestUtils.getCompleteRequestUrl(req));
   >           mav.addObject("timestamp", new Date());
   >           mav.setViewName(DEFAULT_ERROR_VIEW);
   >           return mav;
   >       }}
   >   
   >   ```

2. [springboot和spring的区别](https://www.jianshu.com/p/4784b4fabd0e)

   >- Spring 是一站式的轻量级的java开发框架，核心是控制反转（IOC）和面向切面（AOP），针对于开发的WEB层(springMvc)、业务层(Ioc)、持久层(jdbcTemplate)等都提供了多种配置解决方案。
   >
   >- springMVC是spring基础之上的一个MVC框架，主要处理web开发的路径映射和视图渲染，属于spring框架中WEB层开发的一部分
   >
   >- Spring boot，Spring Boot本身并不提供Spring框架的核心特性以及扩展功能。它是一种基于约定优于配置的理念，简化了spring的配置流程，降低了项目搭建的复杂度，更快的搭建服务。 因为 Spring 的配置非常复杂，各种XML、 JavaConfig、处理起来比较繁琐。springboot简化简化配置。

# springcloud

# springMVC

1. [springmvc的原理流程](https://www.cnblogs.com/wang-meng/p/5701987.html)

   > - 客户端请求提交到DispatcherServlet
   >
   > - 由DispatcherServlet控制器查询HandlerMapping，找到并分发到指定的Controller中。
   > - Controller调用业务逻辑处理后，返回ModelAndView
   > - DispatcherServlet查询一个或多个ViewResoler视图解析器，找到ModelAndView指定的视图
   > - 视图负责将结果显示到客户端

# spring

[ioc的源码解析](https://javadoop.com/post/spring-ioc)

[Spring常见问题](http://blog.csdn.net/qq1137623160/article/details/71194429) 

1. [BeanFactory和ApplicationContext有什么区别](https://www.jianshu.com/p/fd8e441b98c8)

   > - BeanFactory和ApplicationContext是Spring的两大核心接口，都可以当做Spring的容器。其中ApplicationContext是BeanFactory的子接口。
   >
   > 1. BeanFactory：是Spring里面最底层的接口，包含了各种Bean的定义，读取bean配置文档，管理bean的加载、实例化，控制bean的生命周期，维护bean之间的依赖关系。ApplicationContext接口作为BeanFactory的派生，除了提供BeanFactory所具有的功能外，还提供了更完整的框架功能：
   >
   >    ①继承MessageSource，因此支持国际化。
   >
   >    ②统一的资源文件访问方式。
   >
   >    ③提供在监听器中注册bean的事件。
   >
   >    ④同时加载多个配置文件。
   >
   >    ⑤载入多个（有继承关系）上下文 ，使得每一个上下文都专注于一个特定的层次，比如应用的web层。
   >
   > 2. ①BeanFactroy采用的是延迟加载形式来注入Bean的，即只有在使用到某个Bean时(调用getBean())，才对该Bean进行加载实例化。这样，我们就不能发现一些存在的Spring的配置问题。如果Bean的某一个属性没有注入，BeanFacotry加载后，直至第一次使用调用getBean方法才会抛出异常。springApplicationContext容器启动时会实例化非懒加载和单例的bean；
   >
   > 3. BeanFactory通常以编程的方式被创建，ApplicationContext还能以声明的方式创建，如使用ContextLoader。
   >
   > 4. BeanFactory和ApplicationContext都支持BeanPostProcessor、BeanFactoryPostProcessor的使用，但两者之间的区别是：BeanFactory需要手动注册，而ApplicationContext则是自动注册。

2. spring的好处

   > - 轻量： Spring 是轻量的，基本的版本大约2MB。
   > - 控制反转： Spring通过控制反转实现了松散耦合，对象们给出它们的依赖，而不是创建或查找依赖的对象们。
   > - 面向切面的编程(AOP)： Spring支持面向切面的编程，并且把应用业务逻辑和系统服务分开；
   > - 容器： Spring 包含并管理应用中对象的生命周期和配置。
   > - MVC框架： Spring的WEB框架是个精心设计的框架，是Web框架的一个很好的替代品。
   > - 事务管理： Spring 提供一个持续的事务管理接口，可以扩展到上至本地事务下至全局事务（JTA）。
   > - 异常处理： Spring 提供方便的API把具体技术相关的异常（比如由JDBC，Hibernate or JDO抛出的）转化为一致的unchecked 异常

3. BeanFactory 实现举例/applicationContext实现举例

   > Bean 工厂是工厂模式的一个实现，提供了控制反转功能，用来把应用的配置和依赖从正真的应用代码中分离。最常用的BeanFactory 实现是XmlBeanFactory 类。
   >
   > FileSystemXmlApplicationContext、ClassPathXmlApplicationContext、WebXmlApplicationContext

4. spring的注入方式

   >- **构造器依赖注入**
   >- 接口注入
   >- setter注入
   >- 最好的解决方案是用构造器参数实现强制依赖，setter方法实现可选依赖

5. 如何给spring容器配置元数据

   > - 基于xml
   > - 基于注解的配置
   > - 基于java config的配置

6. spring支持的bean的作用域

   > Singleton、protype、request、sesstion

7. spring中单例bean是线程安全的吗

   > no

8. spring中bean生命周期的方法

   > The bean 标签有两个重要的属性（init-method和destroy-method）。用它们你可以自己定制初始化和注销方法。它们也有相应的注解（@PostConstruct和@PreDestroy）

9. 多个相同类型的bean注入

   > 将@Qualifier 注解和@Autowire 注解结合使用以消除这种混淆

10. [spring生命周期](https://www.jianshu.com/p/3944792a5fff)

    > 1.启动容器后，对非懒加载且singleton的bean进行实例化；
    > 2.根据bean定义设置属性；
    > 3.实现了BeanNameAware接口接口的话，setBeanName();
    > 4.实现了BeanFactoryAware接口,会回调该接口的setBeanFactory()方法;
    > 5.实现了ApplicationContextAware，则setApplicationContext();
    > 6.实现了BeanPostProcessor接口的话，则会调用postProcessBeforeInitialzation()方法；
    > 7.实现了initializtionBean接口，则会调用afterPropertiesSet()方法；
    > 8.配置了init-method方法，则会执行init-method配置的方法；
    > 9.实现了BeanPostProcessor接口，则会回调该接口的postProcessAfterInitialization()方法；
    > 10.如果Bean实现了DisposableBean接口，则会回调该接口的destroy()方法；

11. [aop详解](https://www.cnblogs.com/hongwz/p/5764917.html)
    [aop实战](https://juejin.im/post/5a55af9e518825734d14813f)

    > `含义`：
    >
    > aop是相对于oop而言的，它是面向切面编程。例如日志、权限，是散在各个对象中的，而面向切面编程就是将那些与业务无关的，各个对象都用到的功能封装成一个切面，以便减少系统的重复代码，降低模块间的耦合度。
    >
    > - 切面：类是对物体特征的抽象，切面就是对横切关注点的抽象；
    > - 连接点：被拦截到的点，因为Spring只支持方法类型的连接点，所以在Spring中连接点指的就是被拦截到的方法；
    > - 通知：指的就是指拦截到连接点之后要执行的代码，通知分为前置、后置、异常、最终、环绕通知五类；
    > - 目标对象：被代理的目标对象；
    > - 织入：将切面应用到目标对象并导致代理对象创建的过程；

12. spring对aop的支持

    > Spring中AOP代理由Spring的IOC容器负责生成、管理，其依赖关系也由IOC容器负责管理。
    >
    > 1. 默认使用Java动态代理来创建AOP代理，这样就可以为任何接口实例创建代理了;
    > 2. 当需要代理的类不是代理接口的时候，Spring会切换为使用CGLIB代理，也可强制使用CGLIB;
    >
    > 步骤：
    >
    > 1. 定义普通业务组件
    > 2. 定义切入点，一个切入点可能横切多个业务组件
    > 3. 定义增强处理，增强处理就是在AOP框架为普通业务组件织入的处理动作

13. [jdk动态代理cglib的区别](https://www.jianshu.com/p/abb674bb418c)

    [jdk动态代理实例](https://blog.csdn.net/yaomingyang/article/details/80981004)

    [CGLIB动态代理实例](https://blog.csdn.net/yhl_jxy/article/details/80633194)

    > JDK动态代理只能对实现了接口的类生成代理，而不能针对类；此时代理对象和目标对象实现了相同的接口，目标对象作为代理对象的一个属性，具体接口实现中，可以在调用目标对象相应方法前后加上其他业务处理逻辑；InvocationHandlet接口实现；
    >
    > CGLIB是针对类实现代理，主要是对指定的类生成一个子类，覆盖其中的方法（继承）；它使用的是`字节码生产技术`，生成的代理类，不能代理被final修饰的属性或者类；
    >
    > jdk创建的快，cglib运行的快；

14. [spring是如何解决循环依赖的](https://www.jianshu.com/p/4463b9b81249)

    > 无法解决通过构造器注入构成的循环依赖，只能抛出BeanCurrentylyInCreationException异常表示循环依赖。
    >
    > 通过Spring容器提前暴露刚完成构造器注入但未完成其他步骤（如setter注入）的bean来完成的。`通过提前暴露一个单例工厂方法，从而使其他bean能够引用到该bean`

# mongodb

1. MongoDB简介

   > `优点`：
   >
   > - MongoDB是非关系型数据库，有数据库、集合、文档的概念；
   >
   > - 使用类似于json格式的bson结构存储文档数据；支持自定义字段，动态创建字段，更适合存储数组和更复杂的结构；
   > - 数据是存储在硬盘上的，但将热数据和索引存在于内存中，使得热数据的查询非常快；但如果索引的大小超过内存则MongoDB会删除一些内存，导致性能急剧下降；
   > - MongoDB可以提供副本集的高可用性。使用mongos、当主副本发生故障时，副本集可以将辅助副本升级为主服务器；
   > - 负载均衡-MongoDB使用分片的概念，通过MongoDB实例之间拆分数据来水平扩展。
   >
   > `缺点`：
   >
   > - 不支持事务；
   > - 使用的是内置函数，不是sql；所以使用node.js操作比较方便；
   > - 和mysql比成熟度相对较低；

# mysql

1. [mysql的innodb和mylsam存储引擎实现区别](https://blog.csdn.net/qq_35642036/article/details/82820178)

   > 1. innodb是支持事务、支持外键等高级功能，带来性能损耗；mylsam是不支持的，所以性能高点；
   > 2. innodb支持行级锁和表锁；mylsam只支持表锁；
   > 4. innodb的主键索引和数据都放到一个数据文件中，是聚集索引；mylsam是索引和数据文件是分开存放的，是非聚集索引；
   > 6. 实现结构上的区别：
   >
   >   - 第一个重大区别是InnoDB的数据文件本身就是索引文件。MyISAM索引文件和数据文件是分离的，索引文件仅保存数据记录的地址。而在InnoDB中，表数据文件本身就是按B+Tree组织的一个索引结构，这棵树的叶节点data域保存了完整的数据记录。这个索引的key是数据表的主键，因此InnoDB表数据文件本身就是主索引。
   >   - 第二个InnoDB的辅助索引data域存储相应记录主键的值而不是地址。换句话说，InnoDB的所有辅助索引都引用主键作为data域，mylsam使用data域中存放的事数据行记录的地址；
   >
   > 5. 查询行数的区别。因为innodb采用了MVCC技术,对于相同的行,可能同时存在多个版本,innodb必须根据查询的时间来过滤掉一些行,才能得出结果,必然要执行全表扫描,而全表扫描是非常耗时的.对于myisam的表,任何行都只有一个版本，所以处理起来很快

2. [数据库事务](https://www.cnblogs.com/fjdingsd/p/5273008.html)

   > - 原子性：是指事务内的所有操作，要么全部成功，要么全部回滚；
   > - 一致性：是指数据库从一个一致性状态变为另一个一致性状态，事务执行前后都处于一致性状态,比如转账的例子转账前后两个账户的钱的总和不变；
   > - 隔离性：多个事务并发执行，各个事务之间要相互隔离，互不影响；
   > - 持久性：指一个事务一旦提交了，对数据的改变就是永久性的，即使数据库服务挂了也不会改变；

3. 事务带来的问题

   > - 脏读：一个事务读取了另一个未提交事务的数据；
   > - 不可重复读：同一个事务多次查询读取到的同一条数据的某个字段不一致，这是被另一个事务修改了，侧重点是修改；
   > - 幻读：同一个事务中，查询的数据的数量不一致，有可能是修改了或者新增，因为另一个事务进行了删除或者新增操作，侧重点是增删。这个用到的查询条件是非主键索引、非唯一索引；

4. 事务的隔离级别

   > - 读未提交：最低级别，任何情况都无法保证；
   > - 读已提交：可避免脏读；
   > - 可重复读：可避免脏读、不可重复读；
   > - 串行化: 可避免脏读、幻读、不可重复读；

5. 你所了解的mysql索引

   

6. 数据库的优化总结

   > - 注意使用索引，where、join、order by、group by、sum、count、in、distinct 字段中使用索引；
   > - 频繁变化的字段不适合作为索引，维护索引带来的性能损耗太大；
   > - 联合索引注意最左索引 ？？？
   > - order by a,b 两个字段都是降序或者升序，否则用不到索引；
   > - 尽量使用覆盖索引；
   > - 尽量使用not null约束，应为null会消耗额外的空间记录它是否为空；
   > - 尽量避免使用子查询；
   > - 不要对where字段进行表达式计算；
   > - 不要使用!= <>,可以使用between或者in代替，否则用不到索引；
   > - 长字段索引使用前缀索引；
   > - 对表记录进行水平拆分分表
   > - 对表字段多的结构进行垂直拆分；
   > - 选择合适的字段类型，比如主键尽量选择自增id,guid比较长，占空间以及太长查找起来比较慢；datetime占用8个字节，而timestamp占用4个字节，只用了一半，而timestamp表示的范围是1970—2037；
   > - 文件和图片使用文件系统存储，数据库只存储地址；
   > - 批量操作，尽量避免频繁读写
   > - 数据库尽量使用集群，读写分离；

7. explain进行sql分析 ？？？？

8. [关于SQL数据库中的范式](https://blog.csdn.net/sinat_35512245/article/details/52923516)

   > - 第一范式：强调的是列的原子性，即不能再分成其它几列；
   > - 第二范式：一是表必须有一个主键；二是没有包含在主键中的列必须完全依赖于主键，而不能只依赖于主键的一部分；
   > - 第三范式：另外非主键列必须直接依赖于主键，不能存在传递依赖。即不能存在：非主键列 A 依赖于非主键列 B，非主键列 B 依赖于主键的情况；

9. [mysql锁的分类](https://blog.csdn.net/qq_34337272/article/details/80611486)

   > - 表级锁粒度最大，加锁资源消耗少，最简单，触发锁的冲突高；更新大表中的大批量数据的时候用表锁效率最高；
   >
   > - 行级锁粒度最小，加锁资源消耗大，实现起来复杂，但是表的并发度最大；包括record lock、gap lock（范围锁，防止别的事务新增幻影行）、next-key lock 锁定记录本身以及间隙，可解决幻读问题；
   > - 共享锁：事务T对数据A加上共享锁，其它事务只能对数据A加共享锁，不能加排它锁，获取共享锁的事务只能读取数据，不能修改数据；
   > - 排它锁：事务T对数据A加上排它锁后，其它事务不能对A加任何类型的锁，获取排它锁的事务既可以修改数据也可以读数据；

10. 如何避免死锁

    > innodb的行锁是基于索引实现的，未命中所以则会使用表锁；
    >
    > - 使用表锁；
    > - 同一个事务一次尽量获取所有需要的锁；
    > - 多个程序以相同的顺序访问表；

11. [mysql加锁详解系列](https://www.cnblogs.com/crazylqy/p/7611069.html)

12. mysql在rr隔离级别下如何解决幻读

    > - Repeatable Read隔离级别下，id列上有一个非唯一索引，对应SQL：delete from t1 where id = 10; 首先，通过id索引定位到第一条满足查询条件的记录，加记录上的X锁，加GAP上的GAP锁，然后加主键聚簇索引上的记录X锁，然后返回；然后读取下一条，重复进行。直至进行到第一条不满足条件的记录[11,f]，此时，不需要加记录X锁，但是仍旧需要加GAP锁，最后返回结束。
    >
    > - 什么时候会取得gap lock或nextkey lock  这和隔离级别有关,只在REPEATABLE READ或以上的隔离级别下的特定操作才会取得gap lock或nextkey lock。
    >
    > - mysql 的重复读解决了幻读的现象，但是需要 加上 select for update/lock in share mode 变成当读避免幻读，普通读select存在幻读

13. 与mvcc相关的概念

    > - 快照读：简单的select操作，属于快照读。读取的是记录的可见版本 (有可能是历史版本)，不用加锁。
    >- 当前读：插入/更新/删除操作，属于当前读。读取的是记录的最新版本，并且当前读返回的记录，都会加上锁（悲观锁、排它锁），保证其他事务不会再并发修改这条记录。
    > 
    >- 在MySQL/InnoDB中，所谓的读不加锁，并不适用于所有的情况，而是隔离级别相关的。Serializable隔离级别，读不加锁就不再成立，所有的读操作，都是当前读。

14. MVCC的优点

    > - 多版本并发控制（MVCC）是一种用来解决`读-写冲突`的**无锁并发控制**，也就是为事务分配单向增长的时间戳，为每个修改保存一个版本，版本与事务时间戳关联，`读操作只读该事务开始前的数据库的快照`；
    > - 在并发读写数据库时，可以做到在读操作时不用阻塞写操作，写操作也不用阻塞读操作，提高了数据库并发读写的性能；

15. [mysql是如何实现mvcc的](https://blog.csdn.net/sofia1217/article/details/50778906)  

     [mysql的mvcc详细实现](https://blog.csdn.net/SnailMann/article/details/94724197)

    > MVCC模型在MySQL中的具体实现则是由 **`3个隐式字段`**，**`undo日志`** ，**`Read View`** 等去完成的。
    >
    > 1. DATA_TRX_ID（事务id）：标识最近修改本行记录的事务标识符；
    >
    > 2. DATA_ROLL_PTR（回滚指针）：回滚的事务段，undo log record(撤销日志记录)，就是重建该行之前的内容；
    > 3. DB_ROW_ID：隐含的自增ID（隐藏主键），如果数据表没有主键，InnoDB会自动以`DB_ROW_ID`产生一个聚簇索引；
    >
    > `mvcc有以下特点`：MVCC多版本并发控制指的是 **“维持一个数据的多个版本，使得读写操作没有冲突”** 
    >
    > - 乐观锁；
    >
    > - 每行数据都存储一个版本，每行数据更新时都更新版本；
    > - 修改时copy出当前数据，各个事务之间无干扰；
    > - 保存时比较当前版本，成功则覆盖原纪录；失败则放弃（copy、rollback）；
    >
    > `innodb的实现mvcc修改记录的方式`：
    >
    > - 用排它锁锁定该行；
    >
    > - 把该行修改前的值copy到undo Log中；
    >
    > - 修改当前行的值，填写事务号，使回滚指针指向undo log中的修改前的行，如果失败就rollback；
    >
    > - 记录redo日志，包括undo log中的变化；
    >
    > `读视图`：Read View就是事务进行`快照读`操作的时候生产的`读视图`(Read View)，在该事务执行的快照读的那一刻，会生成数据库系统当前的一个快照，记录并维护系统当前活跃事务的ID；
    >
    > `mvvc的标准实现和innodb的实现区别`
    >
    > Innodb的实现真算不上MVCC，因为并没有实现核心的多版本共存，undo log中的内容只是串行化的结果，记录了多个事务的过程，不属于多版本共存。但理想的MVCC是难以实现的，当事务仅修改一行记录使用理想的MVCC模式是没有问题的，可以通过比较版本号进行回滚；但当事务影响到多行数据时，理想的MVCC据无能为力了。理想MVCC难以实现的根本原因在于企图通过乐观锁代替二段提交。修改两行数据，但为了保证其一致性，与修改两个分布式系统中的数据并无区别，而二段提交是目前这种场景保证一致性的唯一手段。`二段提交的本质是锁定，乐观锁的本质是消除锁定`，二者矛盾。

16. RC,RR级别下的InnoDB快照读有什么不同？

    > - 在RR级别下的某个事务的对某条记录的第一次快照读会创建一个快照及Read View, 那么之后的快照读使用的都是同一个Read View；
    > - RC级别下的，事务中，每次快照读都会新生成一个快照和Read View, 这就是我们在RC级别下的事务中可以看到别的事务提交的更新的原因；

17. [数据库为什么要用B+树结构--MySQL索引结构的实现](https://blog.csdn.net/bigtree_3721/article/details/73650601)、

    [mysql的索引数的原理解析](https://blog.csdn.net/u013967628/article/details/84305511)

    > - 首先索引要满足支持根据某个值`快速查找；其次索引要满足根据区间值来查找；
    >   1. 散列表支持O1的根据某个值查找，但是他不支持根据区间范围来查找；
    >   2. 平衡二叉查找树也是支持olog2n的时间复杂度的查找，而且根据中序遍历输出有序序列，但是也不支持按照区间进行查找；红黑树是平衡二叉树的一种，他的h太高，且它的逻辑上很近的节点物理上很远，无法使用局部性原理；
    >   3. 跳表支持，跳表是在链表之上加上多层索引构成的。它支持快速地插入、查找、删除数据，对应的时间复杂度是O(logn)。并且，跳表也支持按照区间快速地查找数据。我们只需要定位到区间起点值对应在链表中的结点，然后从这个结点开始，顺序遍历链表，直到区间终点对应的结点为止，这期间遍历得到的数据就是满足区间值的数据。
    > - 索引其实使用一个和跳表差不多的结构，b+tree，他是根据二叉树演化过来的；
    >   - 把叶子节点串在一条链表上，从小到大排序；我们只需要拿区间的起始值，在树中进行查找，当查找到某个叶子节点之后，我们再顺着链表往后遍历，直到链表中的结点数据值大于区间的终止值为止。所有遍历到的数据，就是符合区间值的所有数据；
    > - 但是数据量比较大的时候索引文件不可能都放到内存里(1亿条数据每个节点占用16字节则需要1GB空间)，只能存储到硬盘上。所以每次查询的时候需要从硬盘上读取节点的数据（索引的结构就要尽量减少磁盘I/O的次数），而树的高度越低，磁盘的io次数越低，此时就需要增大数的度。
    > - 但度也不是越大越好，由于操作系统有页的概念，一次都要读取一页的数据(一页的数据就是一次IO)。根据局部性原理（当一个数据被用到时，其附近的数据也通常会马上被使用）以及磁盘预读，预读的长度一般为页的整数倍，数据库系统巧妙的利用这两个原理。将一个节点的大小设计为一个页的大小；
    > - 而红黑树这种结构，h明显要深的多。由于逻辑上很近的节点（父子）物理上可能很远，无法利用局部性，而B+树每次新建节点时，直接申请一个页的空间，这样就保证一个节点物理上也存储在一个页里

18. [B+树的缺点](https://blog.csdn.net/dbanote/article/details/8897599)

    > B+树最大的性能问题是会产生大量的随机IO，随着新数据的插入，叶子节点会慢慢分裂，逻辑上连续的叶子节点在物理上往往不连续，甚至分离的很远，但做范围查询时，会产生大量读随机IO。

19. [分布式id生成器](https://tech.meituan.com/2017/04/21/mt-leaf.html)

    [分布式id生成器简介2](https://mp.weixin.qq.com/s/7RQhCazoLJ-qO7CglZ6b2Q)

    > 1. snowflake方案：64bit（1bit不用，41bit用表示时间，10bit表示机器，12bit自增序列id），理论上snowflake方案的QPS约为409.6w/s，保证任一机器任一毫秒内生产的id都是不同的；优点是根据时间生成，自增列在低位，递增趋势，不依赖第三方系统；缺点是`强烈依赖机器时钟`；
    > 2. UUID(Universally Unique Identifier)的标准型式包含32个16进制数字，`优点:`是性能非常高，本地生成，没有网络消耗；全球唯一；`缺点:`存储空间大，不易存储；基于mac地址生产，造成mac地址泄漏；无法保证递增趋势；
    > 3. mysql自增主键：存在单点问题；
    > 4. mysql多实例自增主键：每个实例的起始值不同，步长相同；  1+step；2+step；3+step；4+step；`缺点是`:不容易扩容
    > 5. redis生产方案：使用incr原子操作。年月日时分秒+自增id；10万个请求获取id，并发执行完9s左右；`性能一般，占用带宽`
    >

# 网络

[网络学习指南](https://www.jianshu.com/p/45d27f3e1196)

1. http相关

   > - http是无状态的，就是同一个客户端第二次访问同一个服务器页面时，无法知道客户端曾经访问过；
   > - http1.0是非持久连接，每一个客户端必须为每一个请求创建一个新的连接；http1.1使用了keeplive，所谓持久连接就是服务器在发送响应后的一段时间保持这种链接，供其它请求使用；

2. [一个http请求从浏览器输入url后的过程](https://segmentfault.com/a/1190000006879700)

   > DNS域名解析 (要依次查询浏览器缓存、系统缓存、路由器缓存、dns)--> 发起TCP的三次握手 --> 建立TCP连接后发起http请求 --> 服务器响应http请求，浏览器得到html代码 --> 浏览器解析html代码，并请求html代码中的资源（如js、css、图片等） --> 浏览器对页面进行渲染呈现给用户-->断开tcp连接

3. [HTTP与HTTPS的区别](http://www.mahaixiang.cn/internet/1233.html)

   > - https协议需要申请ca证书，一般免费的较少，所以需要一定费用；
   > - http是超文本传输协议，是明文传输；https则是具有安全性的ssl加密传输协议；
   > - 端口不同 80和443；
   > - http的连接很简单是无状态的，https协议是由ssl+http协议加密传输，身份认证的网络协议比较安全；

4. [TCP和UDP的区别](https://blog.csdn.net/sifanchao/article/details/82285018) 

   [TCP和UDP的区别2](https://blog.csdn.net/Li_Ning_/article/details/52117463)

   [深入理解两者的区别](https://blog.csdn.net/striveb/article/details/84063712)

   > - UDP协议和TCP协议都是传输层协议。
   >
   > - 不同点：
   >
   >   1）TCP提供面向连接的传输，通信前要先建立连接（三次握手机制）； UDP提供无连接的传输，通信前不需要建立连接。
   >   2） TCP提供全双工的可靠的传输（有序，无差错，不丢失，不重复）； UDP提供不可靠的传输。
   >   3） TCP面`向字节流`的传输，因此它能将信息分割成组（报文段），并在接收端将其重组； UDP是面向数据报的传输，没有分组开销。
   >   4） TCP提供拥塞控制和流量控制机制； UDP不提供拥塞控制和流量控制机制。
   >
   > - TCP（HTTP、HTTPS、SSH、Telnet、FTP、SMTP）
   >
   > - UDP：（NFS: 网络文件系统、TFTP: 简单文件传输协议、DHCP: 动态主机配置协议、BOOTP: 启动协议(用于无盘设备启动)、DNS: 域名解析协议）

5. UDP

   > - **UDP数据报最大长度64K（包含UDP首部），如果数据长度超过64K就需要在应用层手动分包，UDP无法保证包序，需要在应用层进行编号。**
   > - 无连接：知道对端的IP和端口号就直接进行传输, 不需要建立连接。
   > - 不可靠：没有确认机制, 没有重传机制; 如果因为网络故障该段无法发到对方, UDP协议层也不会给应用层返回任何错误信息。
   > - 面向数据报：不能够灵活的控制读写数据的次数和数量，应用层交给UDP多长的报文, UDP原样发送, 既不会拆分, 也不会合并。
   > - 数据收不够灵活，但是能够明确区分两个数据包，避免粘包问题。![img](https://img-blog.csdn.net/20180901091529706?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpZmFuY2hhbw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

6. [网络分层](https://www.cnblogs.com/duanwandao/p/9941411.html)

   > - 七层模型：物理层、数据链路层、网络层、传输层、会话层、表示层、应用层；
   >
   > - 五层模型：物理层、网络接口层、网络层、传输层、应用层
   >
   > - 物理层：网卡，网线，集线器，中继器，调制解调器
   >
   >   数据链路层：网桥，交换机
   >
   >   网络层：路由器

7. [三次握手四次挥手](https://blog.csdn.net/qzcsu/article/details/72861891)

   ![img](https://img-blog.csdn.net/20180901094250499?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpZmFuY2hhbw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

   > `三次握手`：
   >
   > - 第一次握手：建立连接时，客户端A发送SYN包（SYN=j）到服务器B，并进入SYN_SEND状态，等待服务器B确认
   > - 第二次握手：服务器B收到SYN包，必须确认客户A的SYN（ACK=j+1），同时自己也发送一个SYN包（SYN=k），即SYN+ACK包，此时服务器B进入SYN_RECV状态
   > - 第三次握手：客户端A收到服务器B的SYN＋ACK包，向服务器B发送确认包ACK（ACK=k+1），此包发送完毕，完成三次握手。
   >
   > `四次挥手`：由于TCP连接是全双工的，因此每个方向都必须单独进行关闭
   >
   > - 客户端A发送一个FIN，用来关闭客户A到服务器B的数据传送。
   > - 服务器B收到这个FIN，它发回一个ACK，确认序号为收到的序号加1。
   > - 服务器B关闭与客户端A的连接，发送一个FIN给客户端A。
   > - 客户端A发回ACK报文确认，并将确认序号设置为收到序号加1。
   >
   > `TIME_WAIT状态`：
   >
   > - TCP协议规定,主动关闭连接的一方要处于`TIME_ WAIT`状态**,等待两个MSL(最大报文生存周期)**的时间后才能回到CLOSED状态
   > - 服务器方要处理大量的客户端的连接（生命周期短。但是每秒很多客户端请求）；这个时候如果服务端主动关闭连接，则会出现大量的time_wait状态；
   >
   > `三次握手和四次挥手`：在TCP连接中，服务器端的SYN和ACK向客户端发送是一次性发送的，而在断开连接的过程中， B端向A端发送的ACK和FIN是分两次发送的。因为在B端接收到A端的FIN后， B端可能还有数据要传输，所以先发送ACK，等B端处理完自己的事情后就可以发送FIN断开连接了。
   >

8. tcp如何保证可靠传输 ***

   > - 序列号：TCP将每个字节的数据都进行了编号，即为序列号。
   >
   > - 确认应答：每一个ACK都带有对应的确认序列号，意思是告诉发送者，我已经收到了哪些数据；
   >
   > - 超时重传 、去重：主机A发送数据给B之后, 可能因为网络拥堵等原因, 数据无法到达主机B; 如果主机A在一个特定时间间隔内没有收到B发来的确认应答, 就会进行重发；如果收到重复的数据则会去重；
   >
   > - 拥塞控制：
   >
   >   		- 滑动窗口：建立连接时，各端分配一个缓冲区用来存储接收的数据，并将缓冲区的尺寸发送给另一端。接收方发送的确认消息中包含了自己剩余的缓冲区尺寸。剩余缓冲区空间的数量叫做窗口。其实就是建立连接的双方互相知道彼此剩余的缓冲区大小；
   >     		- 流量控制：接收端处理数据的速度是有限的。 如果发送端发的太快, 导致接收端的缓冲区被打满, 这个时候如果发送端继续发送, 就会造成丢包, 继而引起丢包重传等等一系列连锁反应。
   >     - 延迟应答：如果接收数据的主机立刻返回ACK应答, 这时候返回的窗口可能比较小.
   >       窗口越大, 网络吞吐量就越大, 传输效率就越高. 我们的目标是在保证网络不拥塞的情况下尽量提高传输效率;
   >     		- 捎带应答：在延迟应答的基础上, 我们发现, 很多情况下, 客户端服务器在应用层也是 “一发一收” 的；意味着客户端给服务器说了 “How are you”, 服务器也会给客户端回一个 “Fine, thank you”; 那么这个时候ACK就可以搭顺风车, 和服务器回应的 “Fine, thank you” 一起回给客户端。
   >
   >   

9. **TCP粘包问题**

   > `描述`：
   >
   > - 首先要明确, 粘包问题中的 “包” , 是指的应用层的数据包；
   > - 在TCP的协议头中, 没有如同UDP一样的 “报文长度” 这样的字段, 但是有一个序号这样的字段；
   > - 站在传输层的角度, TCP是一个一个报文过来的，按照序号排好序放在缓冲区中；
   > - 站在应用层的角度, 看到的只是一串连续的字节数据. 那么应用程序看到了这么一连串的字节数据, 就不知道从哪个部分开始到哪个部分是一个完整的应用层数据包；
   >
   > `解决`：
   >
   > - 对于定长的包, 保证每次都按固定大小读取即可;
   > - 对于变长的包, 可以在报头的位置, 约定一个包总长度的字段, 从而就知道了包的结束位置;
   > - 对于变长的包, 还可以在包和包之间使用明确的分隔符

10. [tcp/ip协议](https://developer.51cto.com/art/201906/597961.htm) 

11. session和cookie的区别

    > session和cookie主要是为了解决http请求无状态的问题；
    >
    > - Cookie可以让服务端跟踪每个客户端的访问，但是每次客户端的访问都必须传回这些Cookie，如果Cookie很多，则无形的增加了客户端与服务端的数据传输量，
    > - 而Session则很好地解决了这个问题，同一个客户端每次和服务端交互时，将数据存储通过Session到服务端，不需要每次都传回所有的Cookie值，而是传回一个ID，每个客户端第一次访问服务器生成的唯一的ID，客户端只要传回这个ID就行了，这个ID通常为NAME为JSESSIONID的一个Cookie。这样服务端就可以通过这个ID，来将存储到服务端的KV值取出了。

12. 长连接和短连接

    > HTTP的长连接和短连接本质上是TCP长连接和短连接。HTTP属于应用层协议，在传输层使用TCP协议，在网络层使用IP协议。 IP协议主要解决网络路由和寻址问题，TCP协议主要解决如何在IP层之上可靠地传递数据包，使得网络上接收端收到发送端所发出的所有包，并且顺序与发送顺序一致
    >
    > 

# 数据结构

1. 数组

   > 线性结构、连续内存、O(1)查找、增删需要移动元素O(n)。扩容需要新建一个数组copy旧元素；

2. 链表

   > 线性结构、不是连续内存。通过指针相连；增删比较快O(1)，查找指定元素比较慢 O(n)。

3. 树

   > - 满二叉树：一个深度为n的树，有2的n次方-1个节点的都是满二叉树；
   >
   > - 完全二叉树：完全二叉树是由满二叉树引出来的。一个深度为h的树，除第 h 层外，其它各层 (1～h-1) 的结点数都达到最大个数，第h 层所有的结点都连续集中在最左边，这就是完全二叉树。
   >
   > - 二叉查找树：也叫二叉排序树、二叉搜索树；左子节点小于父亲节点、右子节点大于父亲节点；
   >
   > - 平衡二叉树：为了解决二叉查找树退化成线性结构，平衡二叉树规定，任意节点的左右子树的深度之差的绝对值不能超过1；
   >
   > - [红黑树](https://www.jianshu.com/p/30afcf59828f)：红黑树是一种平衡二叉树。
   >
   >      `特点`：
   >
   >   - 节点是红色或者黑色；
   >   - 根节点一定是黑色；
   >   - 每个叶子节点是黑色的；
   >   - 一个红色节点，他的儿子节点一定是黑色的；
   >   - 每个节点，从该节点到其子孙节点所有路径上包含的相同数目的黑节点；
   >
   >    `插入操作`：
   >
   >   - 由于红黑树是基于二叉排序树的，所以插入也是基于二叉排序树的，即：从根节点开始，遇键值较大者就向左，遇键值较小者就向右，一直到末端，就是插入点；
   >
   >   `修正`：
   >
   >   - 插入节点的父节点和其叔叔节点（祖父节点的另一个子节点）均为红色的；
   >
   >     将当前节点的父节点和叔叔节点涂黑，将祖父节点涂红，再将当前节点指向其祖父节点，再次从新的当前节点开始算法；
   >
   >   - 插入节点的父节点是红色，叔叔节点是黑色，且插入节点是其父节点的左子节点；
   >
   >     操作是把父节点变黑，祖父节点变红，再对祖父节点右旋
   >
   >   - 插入节点的父节点是红色，叔叔节点是黑色，且插入节点是其父节点的右子节点。

4. [b+树](https://ivanzz1001.github.io/records/post/data-structure/2018/06/16/ds-bplustree)  

   > `简介`：b+树是一颗多路查找树，N叉排序树；主要用于数据库和操作系统中，NTFS、ReiserFS、NSS、XFS、JFS、ReFS和BFS等文件系统都在使用`B+树`作为元数据索引。
   >
   > `定义`：
   >
   > 		-  关键字的个数比孩子节点个数少1；
   > 		-  B+树包括内部节点和叶子节点；
   > 		-  B+树和B树的最大不同是内部节点不保存数据，只保存索引，所有数据都保存在叶子节点中；
   > 		-  m阶B+树表示了内部结点最多有m-1个关键字（或者说内部结点最多有m个子树），阶数m同时限制了叶子结点最多存储m-1个记录；
   > 		-  内部结点中的key都按照从小到大的顺序排列；
   > 		-  叶子结点本身依关键字的大小自小而大顺序链接，有指向相邻节点的指针；
   >
   > `特性`：
   >
   > - 所有关键字都出现在叶子节点的链表中，且链表的关键字是有序的；
   > - 不可能是在非叶子节点中命中；
   > - 非叶子节点相当于稀疏索引；
   > - 更适合文件索引系统；

   

# sharding-jdbc

[sharding-jdbc结合mybatis实现分库分表功能](https://www.cnblogs.com/zwt1990/p/6762135.html)

[解读分库分表中间件Sharding-JDBC](https://www.cnblogs.com/duanxz/p/3467106.html)

 1. 分库分表

    >  - 单纯的分表虽然可以解决数据量过大导致检索变慢的问题，但无法解决过多并发请求访问同一个库，导致数据库响应变慢的问题。所以通常水平拆分都至少要采用分库的方式，用于一并解决大数据量和高并发的问题。这也是部分开源的分片数据库中间件只支持分库的原因。
    >
    > - sharding-jdbc
    >
    >  `优点`：
    >
    >  1. 支持各种orm框架：jpa、hibernate、mybatis等
    >  2. 支持各种数据库连接池，dbcp、c3p0、druid等；
    >  3. 轻量级的框架，客户端直连数据库，jar包形式、无代理；
    >  4. 分片策略灵活，支持等号、between、in；
    >  5. 支持聚合、分组、排序、limit、or等操作；
    >
    >  `缺点`：
    >
    >  1. 不支持union以及部分子查询；
    >
    >  `sql改写`：sql在分片环境中执行某些操作是不正确的
    >
    >  - 计算avg计算，以avg1 +avg2+avg3/3计算平均值并不正确，需要改写为（sum1+sum2+sum3）/（count1+count2+ count3）
    >  - 分页，取前10条。每个分片取10条，然后综合再取10条；

​		



# redis 

- 内存淘汰机制

  > 1. volatile-lru：设置过期时间中取最近最少使用的；
  > 2. volatile-ttl：设置过期时间中取将要淘汰的；
  > 3. volatile-random：设置过期时间中任意选取淘汰；
  > 4. allkeys-lru：从全部的key中取最近做少使用；
  > 5. allkeys-random：从全部的key中随机选取；
  > 6. no-enviction：不淘汰数据，抛出异常；

- [redis的LRU过期策略的具体实现](https://zhuanlan.zhihu.com/p/34133067)

  > - 如果使用linkHashMap的实现策略，需要存储额外的next+prev指针，牺牲比较大的内存空间，redis使用的是一个近似的算法，就是随机取出若干个key，然后按照访问时间排序后，淘汰掉最不经常使用的。

- redis的雪崩如何如何解决

  > `事前`：事前采用主从+sentinel哨兵模式，保证failover，避免全盘崩溃；
  >
  > `事中`：使用限流降级措施，使用本地缓存+hystrix限流降级；
  >
  > `事后`：redis持久化，重启服务，从硬盘上回复缓存数据；

- redis的缓存穿透如何解决

  > - 如果缓存的数据是不会更新的，则可以设置为永不失效；
  > - 可以使用定时任务将数据库中的数据放入缓存；
  
- [过期键的删除策略]([http://www.chenwj.cn/2018-01-10/redis%E8%AE%BE%E8%AE%A1%E4%B8%8E%E5%AE%9E%E7%8E%B0-%E6%95%B0%E6%8D%AE%E5%BA%93/](http://www.chenwj.cn/2018-01-10/redis设计与实现-数据库/))

  > 1. 定时删除:
  >
  >    `定义`：在设置键的过期时间的同时,创建一个定时器,让定时器在过期时间来临时,立即执行删除操作；
  >
  >    `优缺点`：定时删除是对内存最友好的，但是是对cpu不友好的。当某一个时刻,有大量的过期键需要删除的时候会占用大量的cpu时间，而此时如果有查询操作,影响查询效率；
  >
  > 2. 惰性删除:
  >
  >    `定义`：放任过期键不管,但每次从键空间获取键时都要检查键是否过期,如果过期则删除;如果没有过期则返回；
  >
  >    `优缺点`：惰性删除对cpu是友好的,只有到了键非删除不可的时候才会被删除.但是对内存是不友好的，相当于内存泄漏；
  >
  > 3. 定期删除:
  >
  >    `定义`： 每个一段时间,程序就会进行一次减产,删除里面的过期键.至于删除多少过期键,怎么检查,由算法决定；
  >
  >    `优缺点`：定期删除时上述两种方式的折中策略,定时删除会每隔一段时间执行一次删除过期键的操作,并通过控制执行的市场和频率来减少对cpu时间的影响;除此之外定期删除还有效的减少了内存浪费。定期删除策略的难点时确定删除操作的执行时间和频率；
  >
  > 4. redis采用`定期删除`和`惰性删除`。

- 持久化（RDB AOF）

  > 1. RDB
  >
  >    - RDB文件是一个经过压缩的二进制文件；
  >    - bgsave命令会派生出一个子进程来创建RDB文件。这期间父进程会处理命令请求。子进程创建完成之后，会通知父进程.。
  >
  >      ```java
  >    save 900 1
  >    save 300 10
  >    save 60 10000
  >     格式：
  >    redis-dbversion-selectDB-0-paris-selctDB-3-paris-EOF-check_sum
  >      ```
  >
  >    - dirty属性记录距离上一次成功执行save和bgsave命令之后，修改操作数；
  >    - lastsave属性时一个时间戳记录距离上一次成功执行save和bgsave命令的时间；
  >
  > 2. AOF
  >
  >    -  当AOF持久化功能打开时，服务器执行完一个写命令，会以协议格式将被执行的写命令追加到服务器状态的aof_buf缓冲区的末尾；
  >
  >    ```
  >    always 将aof_buf缓冲区中的所有内容写入并同步到aof文件
  >    evrysec
  >    no
  >    ```
  >
  >    - `aof重写`： AOF文件存储的是客户端的写命令，随着服务器运行时间越长,文件会越大，系统通过重写来新建一个AOF文件替换旧的文件，新旧的数据是一直的，去除了冗余数据，体积小很多。
  >
  >      通常使用子进程来执行BGREWRITEAOF进行重写；
  >
  >      .

- [redis数据结构的编码]([http://www.chenwj.cn/2018-01-08/redis%E8%AE%BE%E8%AE%A1%E4%B8%8E%E5%AE%9E%E7%8E%B0-%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E4%B8%8E%E5%AF%B9%E8%B1%A13/](http://www.chenwj.cn/2018-01-08/redis设计与实现-数据结构与对象3/))

  > 1. string
  >
  >    - embstr 编码的简单动态字符串：`长度小于等于 39 字节`。它是一种优化版本，将创建字符串对象所需的内存分配次数从 raw 编码的两次降低为一次，它是`只读的`，不可逆的
  >
  >    - raw：简单动态字符串。o(1)获取字符串长度；api安全，不会造成缓冲区溢出（会提前检查是否超出内存）；二进制安全；`如果长度大于39，则使用简单动态字符串存储`
  >    - Int 编码是long 类型的整数：`存储整数`
  >
  > 2. list
  >
  >    - ziplist：`字符串长度小于64byte且数量小于512`
  >
  >      1. 压缩列表是 Redis 为了节约内存而开发的， 由一系列特殊编码的连续内存块组成的顺序型结构
  >
  >      2. 组成：**zlbytes**（占用字节数）、**zltail**（到表尾还有多少距离）、**zllen**（包含节点数）、**entryX**（节点）**zlend**（节点）
  >
  >    - linkedList：双向链表
  >
  > 3. hash
  >
  >    - ziplist`键、值的字符串长度小于64byte且数量小于512`
  >    - hashtable
  >
  >    - rehash扩容
  >    - 渐进式rehash步骤   loadFactor 1，5(执行bgsave操作期间)；
  >      1. 为 ht[1] 分配空间， 让字典同时持有 ht[0] 和 ht[1] 两个哈希表。
  >      2. 在字典中维持一个索引计数器变量 rehashidx ， 并将它的值设置为 `0` ， 表示 rehash 工作正式开始。**rehashidx代表当前rehash的索引**；
  >      3. 在 rehash 进行期间， 每次对字典执行添加、删除、查找或者更新操作时， `程序除了执行指定的操作以外， 还会顺带将 ht[0] 哈希表在 rehashidx 索引上的所有键值对 rehash 到 ht[1]` ， 当 rehash 工作完成之后， 程序将 rehashidx 属性的值增一。
  >      4. 随着字典操作的不断执行， 最终在某个时间点上， ht[0] 的所有键值对都会被 rehash 至 ht[1] ， 这时程序将 rehashidx 属性的值设为`-1` ， 表示 rehash 操作已完成。
  >
  > 4. set
  >
  >    - inset `集合元素都是整数，且个数不超过512`
  >    - hashtable
  >
  > 5. zset
  >
  >    - ziplist `每个元素的大小小于64byte且元素个数小于128个`
  >    - skiplist：
  >
  >    - 跳跃表
  >      1. 跳跃表（skiplist）是一种有序数据结构， 它通过在每个节点中维持多个指向其他节点的指针， 从而达到快速访问节点的目的；
  >      2. 跳跃表支持平均 O(log N) 最坏 O(N) 复杂度的节点查；
  >      3. zset 结构中的 zsl 跳跃表按分值从小到大保存了所有集合元素， 每个跳跃表节点都保存了一个集合元素： 跳跃表节点的 object 属性保存了元素的成员， 而跳跃表节点的 score 属性则保存了元素的分值。 通过这个跳跃表， **程序可以对有序集合进行范围型操作**， 比如 ZRANK 、 ZRANGE 等命令就是基于跳跃表 API 来实现的。
  >      4. zset 结构中的 dict 字典为有序集合创建了一个从成员到分值的映射， 字典中的每个键值对都保存了一个集合元素： 字典的键保存了元素的成员， 而字典的值则保存了元素的分值。 通过这个字典， **程序可以用 O(1) 复杂度查找给定成员的分值， ZSCORE 命令就是根据这一特性实现的**

- [redis分布式锁](https://blog.csdn.net/yb223731/article/details/90349502)

  > redis分布式锁满足的条件：
  >
  > 1. 互斥性。在任意时刻，只有一个客户端能持有锁。
  > 2. 不会发生死锁。即使有一个客户端在持有锁的期间崩溃而没有主动解锁，也能保证后续其他客户端能加锁。
  > 3. 具有容错性。只要大部分的Redis节点正常运行，客户端就可以加锁和解锁。
  > 4. 解铃还须系铃人。加锁和解锁必须是同一个客户端，客户端自己不能把别人加的锁给解了。
  > 5. 如何保证锁的时间大于业务时间；
  > 6. 等待锁的时间不能超过某个时间，即超时失败；
  >
  > 加锁：try   set(lockKey,requestId,nx,expire,second)业务处理的最大时间，
  >
  > 解锁：  lua脚本，
  >
  > ```lua
  > if redis.call('get', KEYS[1]) == ARGV[1] then return redis.call('del', KEYS[1]) else return 0 end"
  > ```




- [redis 的线程模型](https://www.javazhiyin.com/22943.html)

  > - redis内部使用文件事件处理器（file event handler），这个文件事件处理器是单线程的，所以叫做单线程模型。它是使用io多路复用机制同时监听多个socket，根据socket上的事件选择对应的事件处理器。
  > - 文件事件处理器包括：多个socket、io多路复用器、文件事件分配器、文件事件处理器。
  > - 流程：多个socket可能会产生多个操作，每个操作对应的事不同的文件事件。多路复用程序会监听多个socket，将socket产生的时间放入到队列中，时间分配器每次从队列中取出一个事件，把事件交给对应的事件处理器处理。
  >
  
- [单线程支持高并发](https://www.cnblogs.com/javazhiyin/p/10823768.html)

  > - redis是纯内存操作；
  > - redis使用的是非阻塞的io多路复用机制；
  > - 单线程避免了多线程频繁的上下文切换问题；

- redis的应用场景

  > 热点数据的缓存；
  >
  > 限时业务，expire，比如手机验证码；
  >
  > 计数器，incr；
  >
  > sorted set 做排行榜；
  >
  > 分布式锁；
  >
  > 发布、订阅；
  >
  > 存储好友关系，set，取交集共同好友； 
  >
  > setbit bicount  getbit 实现布隆顾虑器；

- 实战 秒杀 ？？？？

  > - 场景：
  >
  > 秒杀前：用户不断刷新商品详情页，页面请求达到瞬时峰值。
  >
  > 秒杀开始：用户点击秒杀按钮，下单请求达到瞬时峰值。
  >
  > 秒杀后：一部分成功下单的用户不断刷新订单或者产生退单操作，大部分用户继续刷新商品详情页等待退单机会。
  >
  > - 面临的问题：①并发太高导致程序阻塞；②库存无法有效控制导致出现超卖的情况；
  >
  > - 基本解决方案：① 数据尽量缓存，阻断和数据库的交互；② 通过锁来控制超卖的情况；
  >
  > - 详细实现：
  >   - 提前预热数据，放入Redis
  >   - 商品列表放入Redis List
  >   - 商品的详情数据 Redis hash保存，设置过期时间
  >   - 用户秒杀存数据Redis sorted set保存，
  >   - 订单产生扣库存通过Redis制造分布式锁，库存同步扣除
  >   - 订单产生后发货的数据，产生Redis list，通过消息队列处理
  >   - 秒杀结束后，再把Redis数据和数据库进行同步

- redis如何实现高可用 

  > 1. 主从复制：数据备份、读写分离、分布式集群；
  >
  >    - 主从复制的全量同步，从库启动后，会向主库发送sync命令；主库会在后台生产rdb文件后发送给从库；从库丢弃旧数据进行载入；主库发送rdb文件后将写命令同时放入缓冲区中；从服务器载入完毕后同事接收来自主服务器的缓冲区的命令；
  >    - 新版复制采用PSYNC命令，具有完整重同步和部分重同步2种操作。主从服务器都会维护一个复制偏移量。
  >    - slaveof 10.211.55.9 6379
  >
  > 2. 哨兵模式：
  >
  >    - 使用sentinal哨兵集群管理多个redis；
  >    - 监控(Monitoring)：哨兵(sentinel) 会不断地检查你的Master和Slave是否运作正常。
  >    - 提醒(Notification)：当被监控的某个Redis出现问题时, 哨兵(sentinel) 会发出通知
  >    - 自动故障迁移(Automatic failover)：当一个Master不能正常工作时，哨兵(sentinel) 会开始一次自动故障迁移操作,它会将失效Master的其中一个Slave升级为新的Master, 并让失效Master的其他Slave改为复制新的Master; 当客户端试图连接失效的Master时,集群也会向客户端返回新Master的地址,使得集群可以使用Master代替失效Master。
  >
  >    `故障转移的具体` ：
  >
  >    - 哨兵(sentinel) 是一个分布式系统,你可以在一个架构中运行多个哨兵(sentinel) 进程,这些进程使用流言协议(gossipprotocols)来接收关于Master是否下线的信息,并使用投票协议(agreement protocols)来决定是否执行自动故障迁移,以及选择哪个Slave作为新的Master.
  >
  >      每个哨兵(sentinel) 会向其它哨兵(sentinel)、master、slave定时发送消息,以确认对方是否”活”着,如果发现对方在指定时间(可配置)内未回应,则暂时认为对方已挂(所谓的”主观认为宕机” Subjective Down,简称sdown).
  >
  >      若“哨兵群”中的多数sentinel,都报告某一master没响应,系统才认为该master"彻底死亡"(即:客观上的真正down机,Objective Down,简称odown),通过一定的vote算法,从剩下的slave节点中,选一台提升为master,然后自动修改相关配置.
  >
  >      虽然哨兵(sentinel) 释出为一个单独的可执行文件 redis-sentinel ,但实际上它只是一个运行在特殊模式下的 Redis 服务器，你可以在启动一个普通 Redis 服务器时通过给定 --sentinel 选项来启动哨兵(sentinel).
  >      
  >
  > 3. cluster模式：
  >    - redis cluster在设计的时候，就考虑到了去中心化，去中间件，加入一个节点就可以获取其它节点；
  >    - Redis 集群**没有使用传统的一致性哈希**来分配数据，而是采用另外一种叫做**哈希槽** (hash slot)的方式来分配的。redis cluster 默认分配了 16384个槽位 ；
  >    - 为了提高高可用，加入了主从模式；

  - [如何保障mysql和redis之间的数据一致](https://zhuanlan.zhihu.com/p/106101091?utm_source=wechat_session)
  
    > - 首先说明，线上使用的是设置的key有超时时间，极端情况是缓存有效时间内是不一致；
    > - 其次，我们采用先删除缓存，然后更新库；
    > - 最后我们会使用canal监控数据库的binLog日志，订阅table的数据变化，如果发生变化发送mq，消费mq删除对应的缓存数据；
  
  
  
  

# kafka [入门](http://blog.csdn.net/hmsiwtv/article/details/46960053)

 [经典试题](https://www.jianshu.com/p/eaafb1581e55)

1. kafka的特性

   >- kafka具有近乎实时的消息处理能力,面对海量消息的查询和存储也能高效的处理。Kafka每秒可以生产约25万消息（50 MB），每秒处理55万消息（110 MB）。
   >- kafka支持消息分区,每个分区中的消息可以保证顺序传输,而分区之间的消息可以并发操作,这样提高了kafka的并发能力；
   >- kafka支持在线增加分区,支持在线水平扩展。
   >- kafka支持为多个分区创建多个副本,其中只会有一个leader副本负责读写,其它副本负责与leader进行同步；
   >- 分布式的部署提高了数据的容灾能力;

2. kafka吞吐量大的原因

   > `顺序读写、零拷贝机制、分区、批量发送、数据压缩`
   >
   > - 计算机组成（划重点）里我们学过，硬盘是机械结构，需要指针寻址找到存储数据的位置，所以，如果是随机IO，磁盘会进行频繁的寻址，导致写入速度下降。Kafka使用了顺序IO提高了磁盘的写入速度，Kafka会将数据顺序插入到文件末尾，避免了随机读写磁盘导致的性能瓶颈。有测试证明多个分区顺序写磁盘的总效率要比随机写内存还要高。顺序结构的存储对于即使数以TB的消息存储也能够保持长时间的稳定性能。
   > - “零拷贝(zero-copy)”系统调用机制，就是跳过“用户缓冲区”的拷贝，建立一个磁盘空间到内存的直接映射，数据不再复制到“用户态缓冲区”，省去了一部比较耗时的工作；.Memory Mapped Files：这个和Java NIO中的内存映射基本相同。  
   > - kafka中的topic中的内容可以被分为多分partition存在,每个partition,所以每次操作都是针对一小部分做操作，很轻便，并且增加并行操作的能力；生产上并发写，消费上多个消费者进消费，提高并发能力；
   > - kafka允许进行批量发送消息，producter发送消息的时候，可以将消息缓存在本地,等到了固定条件发送到kafka；
   > - Kafka还支持对消息集合进行压缩，Producer可以通过GZIP或Snappy格式对消息集合进行压缩压缩的好处就是减少传输的数据量，减轻对网络传输的压力；
   > - 动态增加分区

3. 应用场景

   >- 应用耦合：多应用（服务）间通过消息队列对同一消息进行处理，避免调用接口失败导致整个过程失败；
   >- 限流削峰：广泛应用于秒杀或抢购活动中，避免流量过大导致应用系统挂掉的情况；
   >- 异步处理：多应用对消息队列中同一消息进行处理，应用间并发处理消息，相比串行处理，减少处理时间；
   >- 顺序保证：一般的业务场景中，对消息的顺序的要求还是比较高的，消息队列可以做到；
   >

4. [topic数据量比较多的时候为什么性能急剧下降](http://jm.taobao.org/2016/04/07/kafka-vs-rocketmq-topic-amout/)

   >因为Kafka的每个Topic、每个分区的每个segment都会对应一个物理文件。当Topic数量增加时，消息分散的落盘策略会导致磁盘IO竞争激烈成为瓶颈。而RocketMQ所有的消息是保存在同一个物理文件中的，Topic和分区数对RocketMQ也只是逻辑概念上的划分，所以Topic数的增加对RocketMQ的性能不会造成太大的影响。

5. [kafka如何保证消息不丢失](https://blog.csdn.net/u010627840/article/details/76435385)

   >1. 生产端设置ack=all，各个follower都同步完消息才算成功；在 consumer 端设置 `retries=MAX`，失败后无限重试；
   >
   >2. 消费端采用手动提交commit日志的机制，只有自己手动处理成功，才提交commit日志；
   >
   >3. 由于kafka采用至少一次的机制，保证消息不丢失，有可能重复；
   >   - 落库的数据使用唯一索引的方式保证数据不重复；
   >   - 业务处理逻辑中，将唯一键存储在redis中，消费之前判断是否存在，如果存在则不处理；如果不存在则在处理然后放入redis中；
   
6. 消息队列的对比

   > 单机吞吐量：kafka百万级别；rocketMq是十万级别；activeMQ是万级别的；
   >
   > topic对吞吐量影响：kafka从几十上百的时候，吞吐量下降明显；rocketmq上千的时候吞吐量无变化；
   >
   > 时效性：都是ms级别的，而rabbitMQ是微秒级别的（`erlang`）；
   >
   > 架构：kafka是分布式架构，多副本；rocketMq分布式架构；
   >
   > 可靠性：经过参数优化配置，可以做到 0 丢失，都这样；
   >
   > 功能支持：kafka较为简单；rocketMq功能较为完善，java开发，利于扩展；

7. kafka是如何实现高可用的

   > - 多个broker；topic支持多个partition，每个partition可以在不同的broker上有副本；
   > - 支持副本机制，支持leader选举；假如leader宕机，则可以选举follower担任主节点；
   > - 支持生产者写数据的ack机制；
   > - 消费只会从leader读取，只有所有的follower都被ack了才会被读取到；

8. 大量的消息积压了几个小时还没解决

   > - 先修复consumer的消费问题，确认其没有问题，把所有消费者停了；
   > - 新建一个topic，其partition是原先数量的10倍；
   > - 然后新建一个消费者去分发数据到新建的topic里；
   > - 然后临时征用10个机器来消费，每个消费者消费一个partition中的数据；
   > - 当积压数据消费完之后，恢复原先架构，恢复原先的消费者来消费消息；

9. mq中的消息失效

   > 丢弃旧的数据，重新按照时间点批量写入数据到mq中；

10. mq快写满了

    > 添加分区，添加消费者，加快消费速度；

11. 自己设计一个消息队列

    >- 首先这个 mq 得`支持可伸缩性`吧，就是需要的时候快速扩容，就可以增加吞吐量和容量，那怎么搞？设计个分布式的系统呗，参照一下 kafka 的设计理念，broker -> topic -> partition，每个 partition 放一个机器，就存一部分数据。如果现在资源不够了，简单啊，给 topic 增加 partition，然后做数据迁移，增加机器，不就可以存放更多数据，提供更高的吞吐量了？
    >- 其次你得考虑一下这个 mq 的数据要不要`落地磁盘`吧？那肯定要了，落磁盘才能保证别进程挂了数据就丢了。那落磁盘的时候怎么落啊？顺序写，这样就没有磁盘随机读写的寻址开销，磁盘顺序读写的性能是很高的，这就是 kafka 的思路。
    >- 其次你考虑一下你的 mq 的`可用性`啊？这个事儿，具体参考之前可用性那个环节讲解的 kafka 的高可用保障机制。多副本 -> leader & follower -> broker 挂了重新选举 leader 即可对外服务。
    >- 能不能`支持数据 0`丢失 啊？可以的，参考我们之前说的那个 kafka 数据零丢失方案。
    >- 支持消息的有序应，参考partition；
    
12. [kafka和rocketMq的区别](https://www.cnblogs.com/eryun/p/12088253.html)

    > - 吞吐量：kafka是百万级别的，rocketmq是十万级别的；
    > - 服务治理：kafka使用的是zookeeper做服务发现和治理治理，broker和consumer都会想起注册自身的信息，当有broker或者consumer有宕机的时候回立刻感知，做响应的调整；rocketMq使用自定义的nameServer做服务发现和治理，实时性差点，比如broker宕机，producer和consumer都不能立刻感知，只有下次更新broker建群的时候才能做调整，但数据不会丢失；
    > - 消息查询和延迟队列：rocketmq支持根据offset查询，还支持自定义的key查询；支持延迟队列，rocketmq针对每个topic都有延迟队列，当消费失败后会将消息存入延迟队列中，每个消费者启动的时候回自动订阅延迟队列；
    > - 发送方式：kafka默认使用异步发送的形式，有一个memory buffer暂存消息，同时会将多个消息整合成一个数据包发送，这样能提高吞吐量，但对消息的实效有些影响；rocketmq可选择使用同步或者异步发送；
    > - 刷盘方式：kafka使用的是异步刷盘方式；rocketMq支持同步刷盘，也就是每次消息都刷入盘之后再返，保证消息不丢失；



# [thrift简介](https://www.cnblogs.com/chenny7/p/4224720.html)
[springboot整合thrift](https://blog.csdn.net/lupengfei1009/article/details/100934794)

> `简介`： thrift是`跨语言`的服务部署框架，它通过`IDL语言`来定义RPC的接口和数据类型，然后通过`thrift编译器`生成不同语言的代码。并由生产的代码负责RPC`协议层`和`传输层`的实现。 `TProtocol 协议层`：
>
> - TBinaryProtocol:二进制格式
> - TCompactProtocol:压缩格式，一种更紧凑的二进制格式
> - TJSONProtocol: JSON格式
> - TSimpleJSONProtocol:通过json只写协议，生成的文件很容易通过脚本语言解析；
> - TDebugProtocol:使用易读的可读文本格式，一般debug

> `TTransport 传输层`：定义数据传输格式，可以为TCP/ip传输
>
> - TSocket:阻塞式socket
> - TFramedTransport:以frame为单位进行传输，非阻塞服务中使用
> - TFileTransport: 以文件形式传输
> - TMemoryTransport:将内存用于I/O，java实现时内部实际使用了简单的ByteArrayOutputStream；

> ```
> Thrift支持的服务模型
> ```
>
> - TSimpleServer：简单的单线程的线程模型
> - TThreadPoolServer：多线程服务模型，使用标准的阻塞式IO；
> - TNonblockingServer：多线程服务模型，使用非阻塞式IO（需使用TFramedTransport数据传输方式）
> - THsHaServer，YHsHa引入了线程池去处理（需要使用TFramedTransport数据传输方式），其模型把读写任务放到线程池去处理；

# [nginx反向代理](https://www.jianshu.com/p/bed000e1830b)

> 概念：指以代理服务器来接受internet上的连接请求，然后转发给内部网络上的服务器，并将从服务器上得到的结果返回给一个请求连接的客户端； 优点：
>
> 1. 保护了真实的web服务，对外不可见。外网只能看到反向代理的服务器。
> 2. 节约了有限的IP地址资源，企业内所有的网站共享一个在internet中注册的IP地址，这些服务器分配私有地址，采用虚拟主机的方式对外提供服务。
> 3. 减少WEB服务器压力，提高响应速度；

# zookeeper？

- [zookeeper合集](https://www.cnblogs.com/leeSmall/p/9563547.html)
- [zookeeper简介](https://www.cnblogs.com/wangyayun/p/6811734.html)
- [zookeeper集群搭建](https://www.cnblogs.com/wuxl360/p/5817489.html)
- [zookeeper实现分布式锁](https://www.cnblogs.com/liuyang0/p/6800538.html)
- [zookeeper实现分布式配置文件](https://www.cnblogs.com/leeSmall/p/9614601.html)

# linux服务器？

1. [linux常用命令](https://blog.52itstyle.com/archives/166/)
2. 如何查看端口是否被占用
3. 查看负载

# es简介

1. [简介]([http://www.readingnotes.site/posts/Elasticsearch-%E7%AE%80%E4%BB%8B.html](http://www.readingnotes.site/posts/Elasticsearch-简介.html))

   > es是一个分布式的搜索和分析引擎，用于全文检索、结构化检索和分析；Elasticsearch 基于 Lucene 开发。

2. 常用概念

   > - node：即一个es的运行实例，使用多播或者单播的方式发现cluster并加入；
   > - cluster：包含一个或者多个拥有相同集群名字的node，其中包括一个master node。
   > - index：类比数据库的db，一个逻辑命名空间；
   > - alias：可以给index添加0个或者多个alias，alias给我们提供了一种切换index的能力，不用修改代码；
   > - type：类比关系数据库中的table，一个index可以配置多个type，单一般配置一个；
   > - mapping：类比关系数据库中的schema的概念，mapping 定义了 index 中的 type。mapping 可以显示的定义，也可以在 document 被索引时自动生成，如果有新的 field，Elasticsearch 会自动推测出 field 的type并加到mapping中。
   > - document：类比关系数据库里的一行记录(record)，document 是 Elasticsearch 里的一个 JSON 对象，包括零个或多个field。
   > - field：类比关系数据库里的field，每个field 都有自己的字段类型。
   > - shard：是一个Lucene 实例。Elasticsearch 基于 Lucene，shard 是一个 Lucene 实例，被 Elasticsearch 自动管理。之前提到，index 是一个逻辑命名空间，shard 是具体的物理概念，建索引、查询等都是具体的shard在工作。shard 包括primary shard 和 replica shard，写数据时，先写到primary shard，然后，同步到replica shard，查询时，primary 和 replica 充当相同的作用。replica shard 可以有多份，也可以没有，replica shard的存在有两个作用，一是容灾，如果primary shard 挂了，数据也不会丢失，集群仍然能正常工作；二是提高性能，因为replica 和 primary shard 都能处理查询。另外，shard数和replica数都可以设置，但是，shard 数只能在建立index 时设置，后期不能更改，但是，replica 数可以随时更改。但是，由于 Elasticsearch 很友好的封装了这部分，在使用Elasticsearch 的过程中，我们一般仅需要关注 index 即可，不需关注shard。
   >
   > shard、node、cluster 在物理上构成了 Elasticsearch 集群，field、type、index 在逻辑上构成一个index的基本概念，在使用 Elasticsearch 过程中，我们一般关注到逻辑概念就好，就像我们在使用MySQL 时，我们一般就关注DB Name、Table和schema即可

3. 基础操作

   > - Index: 写document到es中，如果不存在则创建；如果存在则取代旧的；
   >
   > - create：和index不同的是如果存在则抛出异常；
   >
   > - get：根据id获取文档；
   >
   > - update：在Elasticsearch中，更新document时，是把旧数据取出来，然后改写要更新的部分，删除旧document，创建新document，而不是在原document上做修改。
   > - delete：删除文档，只是先标记删除。等Lucene底层进行merge时才会真正把标记删除的文档删除

4. 查询语句

   > - filter与query：官网推荐，仅在全文检索时使用query，其它都是使用filter。
   >
   > - match_all：取出所有文档；
   >
   > - match：一般全文检索时使用；
   >
   > - term/terms：精确匹配；
   >
   > - range：范围查找
   >
   > - exists/missiing：存在和不存在
   >
   > - bool：使用bool 子句来将各种子查询关联起来，组成布尔表达式，bool 子句可以随意组合、嵌套。
   >
   >   ```json
   >   {
   >       "bool" : {
   >           "must" : {
   >               "term" : { "user" : "kimchy" }
   >           },
   >           "must_not" : {
   >               "range" : {
   >                   "age" : { "from" : 10, "to" : 20 }
   >               }
   >           },
   >           "should" : [
   >               {
   >                   "term" : { "tag" : "wow" }
   >               },
   >               {
   >                   "term" : { "tag" : "elasticsearch" }
   >               }
   >           ],
   >           "minimum_should_match" : 1,
   >           "boost" : 1.0
   >       }
   >   }
   >   ```

5. 使用注意事项

   > - **深度分页问题**：Elasticsearch 作为一个分布式搜索与分析引擎，`深度分页问题会带来严重的问题`，给CPU、内存、IO、网络带来巨大压力，所以，在Elasticsearch 不建议使用深度分页，如果要遍历数据，可以采用 SCROLL的方式;
   > - **排序问题**：根据某field排序时，Elasticsearch 会将这个` field 的所有值给加载到内存`，然后，这部分数据会常驻内存，如果数据量大或排序字段多，就会给系统带来巨大压力;
   > - **terms 问题**： terms 里可以传多个值，但是，`量不能太多`，搜索引擎的基本数据结构是倒排索引，terms 里传多个值，原理上来说是查很多的倒排索引，量大了也会给系统带来很大压力。

6. [倒排索引](https://github.com/doocs/advanced-java/blob/master/docs/high-concurrency/es-write-query-search.md)

   > 倒排索引需要先进行分词，然后做单词到文档id数组的映射；
   >
   > - 倒排索引中的所有词项对应一个或多个文档；
   > - 倒排索引中的词项**根据字典顺序升序排列**

7. es写入数据、查询数据的工作原理是什么？

   > - 写入操作
   >   - 客户端选择一个node发送请求，这个node就是cordinating node(协调节点)
   >   - 协调节点根据document取hash路由到对应的node（primary shard）；
   >   - 实际的node上的primary shard处理请求，然后数据同步的replica；
   >   - 协调节点发现primary node和所有的replica都搞定后，就响应给客户端；
   > - 读取数据
   >   - 可以通过 `doc id` 来找一个node查询，coordinate node会根据 `doc id` 进行 hash，判断出来当时把 `doc id` 分配到了哪个 shard 上面去，从那个 shard 去查询。

# vertx

1. [阻塞IO、非阻塞IO、同步IO、异步IO](https://www.jianshu.com/p/2461535c38f3)

   > - 一个io其实分为了两步：发起io请求和实际的io操作；
   > - 阻塞io和非阻塞io的区别在第一步：发起io请求是否被阻塞，如果阻塞直到完成就是传统的阻塞io；
   > - 同步io和异步io的区别在于第二步是否阻塞：如果实际的io读写阻塞请求进程，那么就是同步io；如果不阻塞，而是操作系统帮你完成io操作再返回结果给你就是异步io；

2. [vertx线程实例]([https://colobu.com/2016/03/31/vertx-thread-model/#Vert-x%E7%9A%84%E7%BA%BF%E7%A8%8B%E6%A8%A1%E5%9E%8B](https://colobu.com/2016/03/31/vertx-thread-model/#Vert-x的线程模型))

3. [vertx技术内幕](https://www.sczyh30.com/posts/Vert-x/vertx-advanced-demystifying-thread-model/)

   > - Vert.x 中主要有两种线程：**Event Loop 线程** 和 **Worker 线程**。
   > - 其中，Event Loop 线程结合了 Netty 的 `EventLoop`，用于处理事件。每一个 `EventLoop` 都与唯一的线程相绑定，这个线程就叫 Event Loop 线程
   > - Worker 线程用于执行阻塞任务，这样既可以执行阻塞任务而又不阻塞 Event Loop 线程。
   > - 为了保证线程安全，防止资源争用，Vert.x 保证了某一个 `Handler` 总是被同一个 Event Loop 线程执行，这样不仅可以保证线程安全，而且还可以在底层对锁进行优化提升性能。

# 项目经验类？ 

- fhh自媒体平台
- fhh-service项目
- kafka流平台


- [advanced-java](https://github.com/doocs/advanced-java)

  

# 其它常见试题

 1. 布隆过滤器

> 布隆过滤器是一个位图，主要用于判重。优点是省空间，缺点是存在误判的情况
>
>  set  每次对输入的值进行取hash运算，然后放到对应的位置设置为1。为了解决冲突，可以使用多个hash函数，在对应的bit位设置为1。
>
>  get 单个hash函数则直接判断该bit位是否为1，多个的话需要判断多个bit为的值是否为1，
>
> 
>
> 数据的范围是1到10亿。布隆过滤器的做法是，我们仍然使用一个1亿个二进制大小的位图，然后通过哈希函数，对数字进行处理，让它落在这1到1亿范围内。比如我们把哈希函数设计成f(x)=x%n。其中，x表示数字，n表示位图的大小（1亿），也就是，对数字跟位图的大小进行取模求余。
>
> 不过，你肯定会说，哈希函数会存在冲突的问题啊，一亿零一和1两个数字，经过你刚刚那个取模求余的哈希函数处理之后，最后的结果都是1。这样我就无法区分，位图存储的是1还是一亿零一了。
>
> ​    	为了降低这种冲突概率，当然我们可以设计一个复杂点、随机点的哈希函数。除此之外，还有其他方法吗？我们来看布隆过滤器的处理方法。既然一个哈希函数可能会存在冲突，那用多个哈希函数一块儿定位一个数据，是否能降低冲突的概率呢？我来具体解释一下，布隆过滤器是怎么做的。
>
> 我们使用K个哈希函数，对同一个数字进行求哈希值，那会得到K个不同的哈希值，我们分别记作$X_{1}$，$X_{2}$，$X_{3}$，…，$X_{K}$。我们把这K个数字作为位图中的下标，将对应的BitMap[$X_{1}$]，BitMap[$X_{2}$]，BitMap[$X_{3}$]，…，BitMap[$X_{K}$]都设置成true，也就是说，我们用K个二进制位，来表示一个数字的存在。
>
> 当我们要查询某个数字是否存在的时候，我们用同样的K个哈希函数，对这个数字求哈希值，分别得到$Y_{1}$，$Y_{2}$，$Y_{3}$，…，$Y_{K}$。我们看这K个哈希值，对应位图中的数值是否都为true，如果都是true，则说明，这个数字存在，如果有其中任意一个不为true，那就说明这个数字不存在

[2. 分布式事务TCC](http://ifeve.com/tcc/)

> - 所有事务的参与方都需要实现 try confirm cancle接口；
> - 事务发起方向事务协调器发送事务请求，事务协调器调用所有事务参与这的try方法完成资源的预留；
> - 事务协调器如果发现参与者的try方法失败，则调用参与者的cancle方法，cancle方法要幂等，如果失败重试；
> - 事务协调器如果发现所有的try都ok，则所有参与者都执行confirm操作，直接执行不检查资源是否合适；
> - 协调器如果发现所有的confirm都成功了，则分布式事务结束；
> - 协调器发现有confirm失败了，则协调器会重试；如果一直失败，则进行记录，后续做事务补偿机制；

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







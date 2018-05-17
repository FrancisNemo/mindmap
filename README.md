# mindmap
A simple mind map

Java基础
.   1、	数组和collection
    数组是静态的，先声明，初始化固定的大小，以后就不能修改。
    collection接口，实现了数组动态扩容，数据copy至新数组。

    collection实现类之间的区别
    List 和 Set 的区别
        有序，重复
    List  y, y
    Set  n, n
    这里，不是指数据大小排序，而是有存储结构前后顺序。

.   2、	HashSet 是如何保证不重复的
内部hashmap， Key 实现是Object native hashcode，可能会出现碰撞。
Add/Put的会做处理逻辑：

.   3、	HashMap 为什么不是线程安全的（画图说明）?
      扩容可能会生成环
.   4、HashMap 的扩容过程
    put对象的的时候，检查hashmap的阀值threadhold (0.75\*total)，Resize()按2\*total倍容量扩容，同时rehash。

.   5、HashMap 1.7 与 1.8 的 区别，说明 1.8 做了哪些优化，如何优化的？
    增加红黑树，当单个列表超过8的时候，转换为红黑树。
    Hash算法本质上就是三步：取key的hashCode值、高位运算、取模运算。1.8在hash高位运算做了优化，通过hashCode()的高16位异或低16位实现的：(h = k.hashCode()) ^ (h >>> 16)
    http://www.importnew.com/20386.html
.   6、final finally finalize()

.   7、强引用 、软引用、 弱引用、虚引用
    强度依次减弱。设计这4个的目的是针对不同的gc条件。。
    强引用对象不能被gc回收， 是常见是的赋值操作的变量；
    软引用,在内存不够gc回收
    弱引用，被标记后gc回收
    虚引用，扫描到直接gc回收。
    除强引用外，其他的引用实现都会有关联一个队列.

.   8、Java反射
    动态获取程序在运行时class信息的一种机制
    1 obj.getClass();
    2 任何数据类型（包括基本数据类型）都有一个“静态”的class属性
    3 通过Class类的静态方法：forName（String  className）(常用)

.   9、Arrays.sort 实现原理和 Collection 实现原理

10、LinkedHashMap的应用
11、cloneable接口实现原理

12、异常分类以及处理机制
    编译时受检，
    运行时不受检
13、wait和sleep的区别

线程状态
NEW, 
    RUNNABLE, 
        BLOCKED, 
        WAITING, 
        TIMED_WAITING, 
TERMINATED

BLOCKED是等待获得对象锁进入临界区.
WAITING是调用了不带时间object.wait(), thread.join(), LockSupport.park()
TIMED_WAITING是调用了待时间的 或者 thread.sleep(long)

    wait释放锁 并进入对象的等待队列
    sleep保留锁,
    park对比wait不需要获得锁就可以让线程WAITING，通过unpark唤醒



14、数组在内存中如何分配

JVM
1、synchronized 的实现原理, 静态方法和普通方法的区别, 锁优化，与lock 有什么区别？
    JVM对象监视器，monitorEnter 和 monitorExit指令控制。
    修饰静态方法，则锁住类（所有的对象）。
    修饰普通方法，则锁住当前的对象。（缺点：粒度太粗，其他的线程调用该对象的其他同步方法也会被锁住）
    修饰方法中的代码块，锁住当前代码块。
    
2、volatile 的实现原理？

原子类
6、CAS？CAS 有什么缺陷，如何解决？
    对比交换，实现原子操作
    ABA 问题
11、AQS


锁
21、lock Condition接口及其实现原理
12、如何检测死锁？怎么预防死锁？
预防： tryLock

13、Java 内存模型？
一组指令定义了jvm执行方式

15、线程池的种类，区别和使用场景？
16、分析线程池的实现原理和线程的调度过程？
17、线程池如何调优，最大数目如何确认？
18、ThreadLocal原理，需要注意什么？


同步器
19、CountDownLatch ，semphore, CyclicBarrier 的用法，以及相互之间的差别?


并发容器
8、Hashtable 是怎么加锁的？
9、HashMap 并发问题？
    出现环问题
10、ConcurrenHashMap 介绍？1.8 中为什么要用红黑树？


22、Fork/Join框架的理解

24、八种阻塞队列以及各个阻塞队列的特性


Spring
1、BeanFactory 和 FactoryBean？
2、Spring IOC 的理解，其初始化过程？
3、BeanFactory 和 ApplicationContext？
4、Spring Bean 的生命周期，如何被管理的？
5、Spring Bean 的加载过程是怎样的？
6、如果要你实现Spring AOP，请问怎么实现？
7、如果要你实现Spring IOC，你会注意哪些问题？
8、Spring 是如何管理事务的，事务管理机制？
9、Spring 的不同事务传播行为有哪些，干什么用的？
10、Spring 中用到了那些设计模式？
11、Spring MVC 的工作原理？
12、Spring 循环注入的原理？
13、Spring AOP的理解，各个术语，他们是怎么相互工作的？
14、Spring 如何保证 Controller 并发的安全？
Netty
1、BIO、NIO和AIO
2、Netty 的各大组件
3、Netty的线程模型
4、TCP 粘包/拆包的原因及解决方法
5、了解哪几种序列化协议？包括使用场景和如何去选择
6、Netty的零拷贝实现
7、Netty的高性能表现在哪些方面
分布式相关
1、Dubbo的底层实现原理和机制
2、描述一个服务从发布到被消费的详细过程
3、分布式系统怎么做服务治理
8、对分布式事务的理解
14、redis/zk节点宕机如何处理
15、分布式集群下如何做到唯一序列号
16、如何做一个分布式锁

4、	接口的幂等性的概念
Get 读，幂等
Post 写，不幂等
5、消息中间件如何解决消息丢失问题
6、Dubbo的服务请求失败怎么处理
7、重连机制会不会造成错误
9、如何实现负载均衡，有哪些算法可以实现？
17、用过哪些MQ，怎么用的，和其他mq比较有什么优缺点，MQ的连接是线程安全的吗
18、MQ系统的数据如何保证不丢失
19、列举出你能想到的数据库分库分表策略；分库分表后，如何解决全表查询的问题
20、zookeeper的选举策略
10、Zookeeper的用途，选举的原理是什么？
11、mysql数据的垂直拆分水平拆分。
12、zookeeper原理和适用场景
13、zookeeper watch机制

21、全局ID
数据库
1、mysql分页有什么优化
2、悲观锁、乐观锁
3、组合索引，最左原则
4、mysql 的表锁、行锁
5、mysql 性能优化
6、mysql的索引分类：B+，hash；什么情况用什么索引
7、事务的特性和隔离级别
缓存
1、Redis用过哪些数据数据，以及Redis底层怎么实现
2、Redis缓存穿透，缓存雪崩
3、如何使用Redis来实现分布式锁
4、Redis的并发竞争问题如何解决
5、Redis持久化的几种方式，优缺点是什么，怎么实现的
6、Redis的缓存失效策略
7、Redis集群，高可用，原理
8、Redis缓存分片
9、Redis的数据淘汰策略


JVM
1、详细jvm内存模型
2、讲讲什么情况下回出现内存溢出，内存泄漏？
3、说说Java线程栈
4、JVM 年轻代到年老代的晋升过程的判断条件是什么呢？
5、JVM 出现 fullGC 很频繁，怎么去线上排查问题？
6、类加载为什么要使用双亲委派模式，有没有什么场景是打破了这个模式？
7、类的实例化顺序
8、JVM垃圾回收机制，何时触发MinorGC等操作
9、JVM 中一次完整的 GC 流程（从 ygc 到 fgc）是怎样的
10、各种回收器，各自优缺点，重点CMS、G1
11、各种回收算法
12、OOM错误，stackoverflow错误，permgen space错误

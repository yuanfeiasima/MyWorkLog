* [http://www.cnblogs.com/xrq730/p/5260294.html](http://www.cnblogs.com/xrq730/p/5260294.html) 个人感悟
* tomcat 集群 synchronizied
* mq 丢消息，多发消息 幂等性
* 高cpu占用问题[http://m.blog.csdn.net/blade2001/article/details/9065985](http://m.blog.csdn.net/blade2001/article/details/9065985)
* b树 b-树 b+树

  * b-树，节点有数据，b+树子节点才有数据
  * b+树叶子节点有指针指向下一叶子节点，提高查找效率，顺序读取和排序
  * b+树的内节点不存储数据信息，因此能够生成的每一层的内节点就会多，对内存的开销小

* java

  * hashmap实现
    * 1.7 hash算法
    * 冲突防止
    * 扩容操作
    * 1.8的实现
  * 对象的访问定位
  * 多线程 lock
  * 内存模型
  * 并发
    * 并发包 线程安全集合 底层原理-- 队列和锁机制
    * 双重检查为什么不安全？--并不能保证在单处理器上或多处理器上顺利运行，原因java平台内存模型允许所谓的‘无需写入’
  * 本地方法 [http://www.cnblogs.com/wade-luffy/p/5813747.html](http://www.cnblogs.com/wade-luffy/p/5813747.html)

* mvcc  间隙锁

* redis 数据类型 sortSet如何实现的排序

  * 有权值字段
  * pipline lua
  * 因为redis单线程执行的，所以一个lua脚本是连贯执行的，然后里面按照操作逐个自己写回滚

  * memcache、redis区别？

  * redis value最大值 string最大512m list最大2^32-1 set 2^32-1 incr 数字 2^64-1

* mq kafka区别

  * mq应该只传指令，不用来传递数据？

  * 大部分MQ的消息是有状态的，通过状态判断是否消费过。kafka是通过记录位置，来判断消费到哪儿的

* acid

* volitle

* 线程池

* 数据库死锁解决

* 线程同步的方式

* 什么是分布式系统 分布式：一个业务分拆多个子业务，部署在不同的服务器上  
  ，集群：同一个业务，部署在多个服务器上

  * 分布式系统对于用户而言，他们面对的就是一个服务器，提供用户需要的服务而已，而实际上这些服务是通过背后的众多服务器组成的一个分布式系统，因此分布式系统看起来像是一个超级计算机一样。

    ```
     例如淘宝，平时大家都会使用，它本身就是一个分布式系统，我们通过浏览器访问淘宝网站时，这个请求的背后就是一个庞大的分布式系统在为我们提供服务，整个系统中有的负责请求处理，有的负责存储，有的负责计算，最终他们相互协调把最后的结果返回并呈现给用户。
    ```

  * 分布式是相对中心化而来，强调的是任务在多个物理隔离的节点上进行。中心化带来的主要问题是可靠性，若中心节点宕机则整个系统不可用，分布式除了解决部分中心化问题，也倾向于分散负载，但分布式会带来很多的其他问题，最主要的就是一致性。

    集群就是逻辑上处理同一任务的机器集合，可以属于同一机房，也可分属不同的机房。分布式这个概念可以运行在某个集群里面，某个集群也可作为分布式概念的一个节点。

* 分布式系统数据一致性 cap base [http://www.jianshu.com/p/1156151e20c8?from=timeline&isappinstalled=0](#)

  * 补偿机制

  * 强一致性，相关表在一个库里，牺牲了扩展性

  * 一致性哈希 [http://blog.csdn.net/cywosp/article/details/23397179](http://blog.csdn.net/cywosp/article/details/23397179) 在memcache分布式存储 数据库分库分表中 都可以用，主要目标是就原来的求余 在进行拓展的时候，转移的数据较少，不需要将所有原数据再次进行hash分配

* 分布式锁 扣减库存

  * 微信红包是这样实现的，对不同的红包/库存分成不同的queue，同一个红包/库存的在一个queue里顺序执行。这样同一个库存就不会超卖

  * tcc

  * 秒杀  [http://blog.csdn.net/zhiguozhu/article/details/50517527](http://blog.csdn.net/zhiguozhu/article/details/50517527)

  * 库存扣多了，到底怎么整 [https://mp.weixin.qq.com/s?\_\_biz=MjM5ODYxMDA5OQ==∣=2651960197&idx=1&sn=2e5c17d521772d28d39f31af5d22b34a&chksm=bd2d06598a5a8f4f9de2da89ba8fab711823935442fc632b65d461c923852485ff392c987568&mpshare=1&scene=23&srcid=06157RQsTuEkEOSl1o7TdTJ0\#rd](https://mp.weixin.qq.com/s?__biz=MjM5ODYxMDA5OQ==&mid=2651960197&idx=1&sn=2e5c17d521772d28d39f31af5d22b34a&chksm=bd2d06598a5a8f4f9de2da89ba8fab711823935442fc632b65d461c923852485ff392c987568&mpshare=1&scene=23&srcid=06157RQsTuEkEOSl1o7TdTJ0#rd)

  * update stock set num=$y where sid=$sid

    升级为：

    update stock set num=$num\_new where sid=$sid and num=$num\_old

    这正是大家常说的“Compare And Set”（CAS），是一种常见的降低读写锁冲突，保证数据一致性的方法。（目前是手动扔一个runtimeException 或者他的子类， spring事务默认在有这个异常的时候进行回滚操作）

* 分布式事务 内部事务 外部事务？

  * [http://www.jianshu.com/p/1156151e20c8?from=timeline&isappinstalled=0](http://www.jianshu.com/p/1156151e20c8?from=timeline&isappinstalled=0)

* http 幂等 [http://www.cnblogs.com/weidagang2046/archive/2011/06/04/idempotence.html](http://www.cnblogs.com/weidagang2046/archive/2011/06/04/idempotence.html)

* 接口去重，接口调用后存储下接口的唯一码，下次调用时校验这个唯一码是否使用过，唯一码可以是订单号之类的，存储可以存在数据库、redis、本地缓存，设置过期时间

* 限流 令牌桶 计数器 滑动窗口 漏桶 --依赖nginx 用的是令牌桶  依赖AtomInteger 用的是计数器

  * [http://jinnianshilongnian.iteye.com/blog/2305117](http://jinnianshilongnian.iteye.com/blog/2305117)
  * guava官方的 Ratelimiter

* mysql

  * 聚簇索引 --顺序结构与数据存储屋里结构一致的一种索引，并且一个表的聚簇索引只能有唯一的一条

    * innoDB中设置与业务无关的自增id，然后设为主键，
    * 因为innoDB是聚簇索引，插入之后b+树不用在平衡，如果该值大小不定，会引起再平衡，影响插入效率
    * 聚簇索引存放的是数据信息，非聚簇索引存放的是指向数据的指针
    * 聚簇索引需要对数据的物理存放进行排序，所以一张表只有一个聚簇索引
    * innoDB引擎下的表都会建立聚簇索引，如果有主键，就用主键，如果没有主键，就找一个非空的唯一索引，如果没有，会自动创建一个隐藏的主键。
    * innodb的主键默认是聚簇索引吗？对， 也可以先设其他值为聚簇索引，再设置主键，主键就不是聚簇索引了吧 对

    * innodb中，聚簇索引是mysql自己来决定的。选择的顺序是：（1）定义了主键，就选择主键；（2）没有主键，选择第一个非空的唯一索引；（3）两者都没有，innodb自己生成一个占6byte的自增长列。然后以它作为聚簇索引列

    * innoDB下的非聚簇索引的叶子节点存放的都是主键id，使用 非主键的索引都会再走一遍主键索引

    * 聚簇索引是基础，表示数据和b+树之间的关系，聚簇索引是对存储在磁盘上的数据重新组织以按照一个或多个列的值排序的算法

  * innoDB 锁原理

    * 只有通过索引条件检索数据，innoDB才使用行级锁，否则InnoDB将使用表锁，在实际开发中应当注意；如果索引建立的不合适，优化器有可能使用表锁
    * 行锁是加在记录上的锁，InnoDB中的记录是以B+树索引的方式组织在一起的，InnoDB的行锁实际是 index record lock，即对B+索引叶子节点的锁。索引可能有多个，因此操作一行数据时，有可能会加多个行锁在不同的B+树上。

  * 最左原则

  * 索引建立技巧

  * for update 是否打开事务

  * 死锁

  * in or 走索引的问题
    * in会走索引，但是如果传入的值不存在是不是不走索引？？
    * or不会走？
  * record lock  gap lock  next-key-lock（nextkeylock对查询范围进行加锁，在另一个事务执行插入操作时是不被执行的，所以避免了幻读） [http://www.jianshu.com/p/bf862c37c4c9](http://www.jianshu.com/p/bf862c37c4c9)
  * 最好避免随机的聚簇索引，特别对于I/O密集型的应用。例如，从性能的角度考虑，使用UUID作为聚簇索引会很糟糕：它使得聚簇索引的插入变得完全随机，这是最坏的情况，使得数据没有任何聚集特性。通过测试，向UUID主键插入行不仅花费的时间更长，而且索引占用的空间也更大。这一方面是由于主键字段更长，另一方面毫无疑问是由于页分裂和碎片导致的。

  * 这个是属于大偏移量分页 select \* from t where id &gt; 10000 limit 10

* 缓存系统设计 缓存击穿 缓存刷新 缓存失效

* spring

  * @Resource的作用相当于@Autowired，只不过@Autowired按byType自动注入，而@Resource默认按 byName自动注入罢了。@Resource有两个属性是比较重要的，分是name和type，Spring将@Resource注解的name属性解析为bean的名字，而type属性则解析为bean的类型。所以如果使用name属性，则使用byName的自动注入策略，而使用type属性时则使用byType自动注入策略。如果既不指定name也不指定type属性，这时将通过反射机制使用byName自动注入策略。
    　　@Resource装配顺序
    　　1. 如果同时指定了name和type，则从Spring上下文中找到唯一匹配的bean进行装配，找不到则抛出异常
    　　2. 如果指定了name，则从上下文中查找名称（id）匹配的bean进行装配，找不到则抛出异常
    　　3. 如果指定了type，则从上下文中找到类型匹配的唯一bean进行装配，找不到或者找到多个，都会抛出异常
    　　4. 如果既没有指定name，又没有指定type，则自动按照byName方式进行装配；如果没有匹配，则回退为一个原始类型进行匹配，如果匹配则自动装配； 
  * dispatchler [http://sishuok.com/forum/blogPost/list/5188.html](http://sishuok.com/forum/blogPost/list/5188.html)
  * 整体处理流程 [http://www.cnblogs.com/plxx/p/5400467.html](http://www.cnblogs.com/plxx/p/5400467.html)
  * springmvc里面自动转化json靠什么？

  * requestMapping的用法 例如矩阵参数 可变参数 必填参数

  * controller 与context的注解分开来扫

  * springEL在bean装载的时候怎么找对象的属性

  * aop怎么实现的 串这aspectJ 可能考察切面表达式

  * core 是啥作用 beans的bean加载过程

  * 事务处理[https://my.oschina.net/u/1415809/blog/209075](https://my.oschina.net/u/1415809/blog/209075)

* dubbo 官方介绍 调用机制，协议，长连接，注册机

* 排序

  * 冒泡 最好n 最坏平均 对数复杂度

  * 快排 对数时间复杂度

* 二分查找

  * bianrySearch

* 设计模式

  * 单例

    * ```java
      public class AtomicSingleton  
       {  
          private static AtomicReference<AtomicSingleton> INSTANCE   
                    = new AtomicReference<>();  
          private AtomicSingleton() {}  

          public static AtomicSingleton getInstace(){  
              AtomicSingleton current = INSTANCE.get();  
              for (;;) {  
                  if(current != null){  
                      return current;  
                  }  
                  current = new AtomicSingleton();  

                  if(INSTANCE.compareAndSet(null, current))  
                  {  
                      return current;  
                  }  

              }  
          }  
      }
      ```

* 工厂模式 --数据库获取连接

* gc案例

  * 场景是这样的 线上应用发现频繁full gc（用发现 jstat -gcutil pid 1000\(采样频率\)）（pid 通过top加 ps-ef就找到了 上面说的那个pid是你需要输入的pid 后面的1000是1s的采样频率），然后用jmap 提取堆内存 发现两个对象占用比例异常

  * 然后就去查找对应的sql，定位到有个sql查询没有参数，进行了全表查询，然后发现一个语句 ParamValidator.isNull\(String a\)

  * 使用的地方传进去的有可能是一个空字串 String a=""

  * 下面执行sql 的时候 mybatis 判断这个地方是""所以就不加这个条件造成了全表查询。造成了内存的过快增加，触发了频繁gc

  * 然后 对象持续在s0 增加 ，触发了cms回收，然后cms回收失败，就触发了full gc

  * 因为查询了一百多万条记录，就有一百万个对象持续的在s0上分配

  * minor gc 如果给的新生代小了 频率会更高 给的新生代大了 频率会低 但是gc时间会变长

* 垃圾回收器   回收器：接口和页面使用CMS+ParNew，保证接口和页面停顿短；作业定时任务使用Parallel Scavenge+Parallel Old，高吞吐量，减少GC消耗的时间比例

  * 回收算法 接口、页面 CMS：老年代、多线程并发、标记清除算法  ParNew：新生代、多线程并行、复制算法 定时任务 Parallel Scavenge：新生代、多线程并、复制算法 Parallel Old：老年代、多线程并行、标记整理算法

* 给定a、b两个文件，各存放50亿个url，每个url各占64字节，内存限制是4G，让你找出a、b文件共同的url？

  方案1：可以估计每个文件安的大小为5G×64=320G，远远大于内存限制的4G。所以不可能将其完全加载到内存中处理。考虑采取分而治之的方法。

  遍历文件a，对每个url求取hash\(url\)%1000，然后根据所取得的值将url分别存储到1000个小文件（记为a0,a1,...,a999）中。这样每个小文件的大约为300M。

  遍历文件b，采取和a相同的方式将url分别存储到1000小文件（记为b0,b1,...,b999）。这样处理后，所有可能相同的url都在对应的小文件（a0vsb0,a1vsb1,...,a999vsb999）中，不对应的小文件不可能有相同的url。然后我们只要求出1000对小文件中相同的url即可。

  求每对小文件中相同的url时，可以把其中一个小文件的url存储到hash\_set中。然后遍历另一个小文件的每个url，看其是否在刚才构建的hash\_set中，如果是，那么就是共同的url，存到文件里面就可以了。

* 



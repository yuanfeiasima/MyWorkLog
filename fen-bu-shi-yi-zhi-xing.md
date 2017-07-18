1. 库存扣减超卖，数据强一致性：可以把`订单和库存`放入同一个数据库分片，利用关系型数据库的强一致性特性（ACID）（同库的转账也可以用这种方法）
2. 跨库转账
3. 一致性哈希[http://blog.csdn.net/cywosp/article/details/23397179](http://blog.csdn.net/cywosp/article/details/23397179)
4. 什么是分布式系统 分布式：一个业务分拆多个子业务，部署在不同的服务器上  
   ，集群：同一个业务，部署在多个服务器上

   * 分布式系统对于用户而言，他们面对的就是一个服务器，提供用户需要的服务而已，而实际上这些服务是通过背后的众多服务器组成的一个分布式系统，因此分布式系统看起来像是一个超级计算机一样。

   * 例如淘宝，平时大家都会使用，它本身就是一个分布式系统，我们通过浏览器访问淘宝网站时，这个请求的背后就是一个庞大的分布式系统在为我们提供服务，整个系统中有的负责请求处理，有的负责存储，有的负责计算，最终他们相互协调把最后的结果返回并呈现给用户。

   * 分布式是相对中心化而来，强调的是任务在多个物理隔离的节点上进行。中心化带来的主要问题是可靠性，若中心节点宕机则整个系统不可用，分布式除了解决部分中心化问题，也倾向于分散负载，但分布式会带来很多的其他问题，最主要的就是一致性。

     集群就是逻辑上处理同一任务的机器集合，可以属于同一机房，也可分属不同的机房。分布式这个概念可以运行在某个集群里面，某个集群也可作为分布式概念的一个节点。

5. 分布式事务 内部事务 外部事务？

   * [http://www.jianshu.com/p/1156151e20c8?from=timeline&isappinstalled=0](http://www.jianshu.com/p/1156151e20c8?from=timeline&isappinstalled=0)

6. 分布式锁 扣减库存

   * 微信红包是这样实现的，对不同的红包/库存分成不同的queue，同一个红包/库存的在一个queue里顺序执行。这样同一个库存就不会超卖

   * tcc

   * 秒杀[http://blog.csdn.net/zhiguozhu/article/details/50517527](http://blog.csdn.net/zhiguozhu/article/details/50517527)

   * 库存扣多了，到底怎么整[https://mp.weixin.qq.com/s?\_\_biz=MjM5ODYxMDA5OQ==∣=2651960197&idx=1&sn=2e5c17d521772d28d39f31af5d22b34a&chksm=bd2d06598a5a8f4f9de2da89ba8fab711823935442fc632b65d461c923852485ff392c987568&mpshare=1&scene=23&srcid=06157RQsTuEkEOSl1o7TdTJ0\#rd](https://mp.weixin.qq.com/s?__biz=MjM5ODYxMDA5OQ==&mid=2651960197&idx=1&sn=2e5c17d521772d28d39f31af5d22b34a&chksm=bd2d06598a5a8f4f9de2da89ba8fab711823935442fc632b65d461c923852485ff392c987568&mpshare=1&scene=23&srcid=06157RQsTuEkEOSl1o7TdTJ0#rd)

   * update stock set num=$y where sid=$sid

     升级为：

     update stock set num=$num\_new where sid=$sid and num=$num\_old

     这正是大家常说的“Compare And Set”（CAS），是一种常见的降低读写锁冲突，保证数据一致性的方法。（目前是手动扔一个runtimeException 或者他的子类， spring事务默认在有这个异常的时候进行回滚操作）

7. 分布式系统数据一致性 cap base   [http://www.jianshu.com/p/1156151e20c8?from=timeline&isappinstalled=0](https://github.com/yuanfeiasima/MyWorkLog/blob/master/bo-wen-shou-cang.md#)

   * 补偿机制

   * 强一致性，相关表在一个库里，牺牲了扩展性

   * 一致性哈希[http://blog.csdn.net/cywosp/article/details/23397179](http://blog.csdn.net/cywosp/article/details/23397179)在memcache分布式存储 数据库分库分表中 都可以用，主要目标是就原来的求余 在进行拓展的时候，转移的数据较少，不需要将所有原数据再次进行hash分配




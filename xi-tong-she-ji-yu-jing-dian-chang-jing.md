1. ###### 给定a、b两个文件，各存放50亿个url，每个url各占64字节，内存限制是4G，让你找出a、b文件共同的url？

   1. 方案1：可以估计每个文件安的大小为5G×64=320G，远远大于内存限制的4G。所以不可能将其完全加载到内存中处理。考虑采取分而治之的方法。

      遍历文件a，对每个url求取hash\(url\)%1000，然后根据所取得的值将url分别存储到1000个小文件（记为a0,a1,...,a999）中。这样每个小文件的大约为300M。

      遍历文件b，采取和a相同的方式将url分别存储到1000小文件（记为b0,b1,...,b999）。这样处理后，所有可能相同的url都在对应的小文件（a0vsb0,a1vsb1,...,a999vsb999）中，不对应的小文件不可能有相同的url。然后我们只要求出1000对小文件中相同的url即可。

      求每对小文件中相同的url时，可以把其中一个小文件的url存储到hash\_set中。然后遍历另一个小文件的每个url，看其是否在刚才构建的hash\_set中，如果是，那么就是共同的url，存到文件里面就可以了。
2. 缓存系统设计 缓存击穿 缓存刷新 缓存失效
3. 限流 令牌桶 计数器 滑动窗口 漏桶 --依赖nginx 用的是令牌桶 依赖AtomInteger 用的是计数器

   * [http://jinnianshilongnian.iteye.com/blog/2305117](http://jinnianshilongnian.iteye.com/blog/2305117)
   * guava官方的 Ratelimiter

4. 接口去重，接口调用后存储下接口的唯一码，下次调用时校验这个唯一码是否使用过，唯一码可以是订单号之类的，存储可以存在数据库、redis、本地缓存，设置过期时间

5. http 幂等

   [http://www.cnblogs.com/weidagang2046/archive/2011/06/04/idempotence.html](http://www.cnblogs.com/weidagang2046/archive/2011/06/04/idempotence.html)

6. tomcat 集群 synchronizied ?

7.库存超卖
   1. 用设值代替扣减 扣减非幂等 设置幂等
   2. cas降低读写锁冲突，提高性能
   3. 比较版本号代替比较值  防止aba问题




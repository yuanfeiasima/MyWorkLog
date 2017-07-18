1. ###### 垃圾回收器：接口和页面使用CMS+ParNew，保证接口和页面停顿短；作业定时任务使用Parallel Scavenge+Parallel Old，高吞吐量，减少GC消耗的时间比例

   * 接口和页面 CMS：老年代、多线程并发、标记清除算法； ParNew：新生代、多线程并行、复制算法 
   * 定时任务 Parallel Scavenge：新生代、多线程并、复制算法； Parallel Old：老年代、多线程并行、标记整理算法
2. ###### gc案例

   * 场景是这样的 线上应用发现频繁full gc（用发现 jstat -gcutil pid 1000\(采样频率\)）（pid 通过top加 ps-ef就找到了 上面说的那个pid是你需要输入的pid 后面的1000是1s的采样频率），然后用jmap 提取堆内存 发现两个对象占用比例异常

   * 然后就去查找对应的sql，定位到有个sql查询没有参数，进行了全表查询，然后发现一个语句 ParamValidator.isNull\(String a\)

   * 使用的地方传进去的有可能是一个空字串 String a=""

   * 下面执行sql 的时候 mybatis 判断这个地方是""所以就不加这个条件造成了全表查询。造成了内存的过快增加，触发了频繁gc

   * 然后 对象持续在s0 增加 ，触发了cms回收，然后cms回收失败，就触发了full gc

   * 因为查询了一百多万条记录，就有一百万个对象持续的在s0上分配

   * minor gc 如果给的新生代小了 频率会更高 给的新生代大了 频率会低 但是gc时间会变长




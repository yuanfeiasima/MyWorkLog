1. tomcat原理配置
2. JAX-RS是什么

3. servlet 容器

4. 看过dubbo-rest， 结论：

   1. 内网优先使用dubbo-rpc,性能要更好

   2. 对于gzip的开启，要考虑cpu的开销，不要得不偿失（通过压测）

   3. 和springMVC的比较，springMVC综合了html输出，restful接口，页面跳转等多个功能，dubbo-rest更适合单纯的服务，且面向外网，跨语言

   4. 官方压测数据（10个并发，传输50k字符串，原样返回没有处理逻辑）

      1. REST: Tomcat + JSON（dubbo-rest + tomcat部署+ json数据格式），平均响应时间2s，4796TPS

      2. Dubbo: fastjson， 平均响应时间1.57s, 6352TPS

5. 原文地址 http://dangdangdotcom.github.io/dubbox/rest.html




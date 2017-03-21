## `项目使用的命令`

```
解压
tar axvf .tar.gz
启动
(chmod 777 leflow)
nohup ./leflow &
```

kafka监控命令

Java -Xms512M -Xmx512M -Xss1024K -XX:PermSize=256m -XX:MaxPermSize=512m -cp KafkaOffsetMonitor-assembly-0.2.0.jar com.quantifind.kafka.offsetapp.OffsetGetterWeb --zk localhost:2181 --port 8086 --refresh 10.seconds --retain 7.days 1&gt;wwt\_kafka/stdout.log 2&gt;wwt\_kafka/stderr.log &

```
测试机器 10.112.156.97
```




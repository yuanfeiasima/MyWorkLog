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

```
索引：workflow
集群名： o2obi

钟成辉 2017/3/20 11:17:15
集群ip:10.118.31.102,10.118.31.103,10.118.31.106,10.118.31.8,10.118.31.9,10.118.31.10,10.118.31.11

http://10.118.31.102:9200/_plugin/head/
```

```
上线：
1.数据库建表初始化，
2.es设置
```

```
写了个自动化部署脚本，以后在开发机直接运行这个命令就行
/letv/deployment/deploy_leflow.sh
```




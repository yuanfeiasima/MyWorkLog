安装总结

1. 设置静态ip NAT模式与宿主机ip无关
2. 配置hostname /etc/init.d/iptables stop   iptable -L \(防火墙还是没关闭\)， service iptables stop\(成功关闭防火墙\) 
3. 避免网络问题 setenforce 0 getenforce\(没生效\)
4. /etc/hosts 
5. ssh-keygen 生成公钥拷贝到authority.key
6. 安装 JDK 配置环境变量 ~/.bashrs\(与当前用户有关\)
7. 安装hadoop，修改配置文件core-site.xml mapred-site.xml hdfs-site.xml
8. 清除tmp logs
9. 格式化namenode  ./hadoop namenode -format 
10. 启动./start-all.sh 使用jps查看进程
11. 验证 ./hadoop fs -ls /   上传文件 ./hadoop fs -put /etc/passwd /  查看文件内容 ./hadoop fs -cat /passwd




安装总结

1. 设置静态ip NAT模式与宿主机ip无关
2. 配置hostname /etc/init.d/iptables stop   iptable -L \(防火墙还是没关闭\)， service iptables stop\(成功关闭防火墙\) 
3. /etc/hosts 
4. 安装JDK 配置环境变量 ~/.bashrs\(与当前用户有关\)
5. 安装hadoop，修改配置文件core-site.xml mapred-site.xml hdfs-site.xml




```
sudo yum -y groupinstall "Development Tools"
```

```
先卸载
rpm -qf /usr/bin/autoconf
rpm -e --nodeps autoconf-2.63
重装
wget http://ftp.gnu.org/gnu/autoconf/autoconf-2.69.tar.gz
tar xvf autoconf-2.69.tar.gz
cd autoconf-2.69
./configure --prefix=/usr
make
sudo make install
cd ..
```

reconf

```
sudo autoreconf -ivf
```

之后重新编译

```
[root@COS1 src]# tar xvf nutcracker-0.3.0.tar.gz
[root@COS1 nutcracker-0.3.0]# cd nutcracker-0.3.0
[root@COS1 src]#./configure 
[root@COS1 nutcracker-0.3.0]# make && make install
```

编辑配置文件

```
[root@COS1 conf]# cd /usr/local/src/nutcracker-0.3.0/conf
[root@COS1 conf]# cp nutcracker.yml /etc/
[root@COS1 conf]# vim /etc/nutcracker.yml
alpha:
  listen: 0.0.0.0:22121
  hash: fnv1a_64
  distribution: ketama
  auto_eject_hosts: true
  redis: true
  server_retry_timeout: 2000
  server_failure_limit: 1
  servers: --两台redis服务器的地址和端口
   - 10.23.22.240:6379:1   
   - 10.23.22.241:6379:1
```

测试配置文件

```
[root@COS1 nutcracker-0.3.0]# nutcracker -t /etc/nutcracker.yml 
nutcracker: configuration file 'conf/nutcracker.yml' syntax is ok
```

启动twemproxy：

```
[root@COS1 nutcracker-0.3.0]# nutcracker  --help
This is nutcracker-0.3.0

Usage: nutcracker [-?hVdDt] [-v verbosity level] [-o output file]
                  [-c conf file] [-s stats port] [-a stats addr]
                  [-i stats interval] [-p pid file] [-m mbuf size]

Options:
  -h, --help             : this help                           
  -V, --version          : show version and exit                 
  -t, --test-conf        : test configuration for syntax errors and exit 
  -d, --daemonize      : run as a daemon                    
  -D, --describe-stats   : print stats description and exit
  -v, --verbosity=N      : set logging level (default: 5, min: 0, max: 11)
  -o, --output=S         : set logging file (default: stderr)
  -c, --conf-file=S      : set configuration file (default: conf/nutcracker.yml) #配置
  -s, --stats-port=N     : set stats monitoring port (default: 22222)
  -a, --stats-addr=S     : set stats monitoring ip (default: 0.0.0.0)
  -i, --stats-interval=N : set stats aggregation interval in msec (default: 30000 msec)
  -p, --pid-file=S       : set pid file (default: off)
  -m, --mbuf-size=N      : set size of mbuf chunk in bytes (default: 16384 bytes)
[root@COS1 nutcracker-0.3.0]# nutcracker -d -c /etc/nutcracker.yml
[root@COS1 nutcracker-0.3.0]# ps -ef|grep nutcracker
root     15358     1  0 02:40 ?        00:00:00 nutcracker -d -c /etc/nutcracker.yml
```

测试twemproxy：

```
[root@COS1 ~]# redis-cli -p 22121
127.0.0.1:22121> get kin
"kin"
127.0.0.1:22121> set kin king
OK
127.0.0.1:22121> get kin
"king"
```

```
http://www.cnblogs.com/haoxinyue/p/redis.html
```

### 使用

```
防火墙
```




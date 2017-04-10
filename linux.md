修改ip 

`路径 /etc/sysconfig/network-scripts`

DEVICE="eth0"

BOOTPROTO="static"

NM\_CONTROLLED="yes"

ONBOOT="yes"

TYPE="Ethernet"

IPADDR=192.168.183.11

NETMASK=255.255.255.0

GATEWAY=192.168.183.2

DNS1=202.106.0.20

重启网络服务 /etc/init.d/network restart




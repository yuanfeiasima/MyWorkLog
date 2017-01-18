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

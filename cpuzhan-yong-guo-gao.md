### **第一种方式**

1. top命令
   1. top： P cpu， M 内存
2. 显示线程列表 ps -mp pid -o THREAD,tid,time
   1. ps -mp 7545 -o THREAD,tid,time
3. printf "%x\n" tid  转换成16进制格式

4. jstack pid \|grep tid -A 30 打印堆栈信息



### **第二种方式**

1. top 命令 找到占用cpu最高的pid
2. top -H -pPID 找到对应的线程， -H 指显示线程，-p 是指定进程
3. jstack -l 2023 &gt; tempfile.txt  2023线程id  在这个文件中能看到线程状态 类 方法信息



### **结果提示：**

Unable to open socket file: target process not responding or HotSpot VM not loaded

The -F option can be used when the target process is not responding

### **原因：**

java的pid文件被删除了，jstack命令读不到信息了。

因为linux系统为了防止tmp目录文件过多，有删除管理机制：tmpwatch

### **解决方式：**

http://zhangshaoxiong.blog.51cto.com/4408282/1310166


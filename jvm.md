-Xmx 最大堆

–Xms 最小堆

-Xmn 新生代大小

-XX:NewRatio 
```
新生代（eden+2*s）和老年代（不包含永久区）的比值

例如：4，表示新生代:老年代=1:4，即新生代占整个堆的1/5
```

-XX:SurvivorRatio 幸存区

```
设置两个Survivor区和eden的比值

例如：8，表示两个Survivor:eden=2:8，即一个Survivor占年轻代的1/10
```
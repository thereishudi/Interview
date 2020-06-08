## 1. CAS

unsafe类

有一个compareAndSwap方法

被native修饰

一直跟踪会到Linux源码 里面有个cmpxchg方法（汇编层）。

`lock comxchg`指令(lock是原子性隔离，comxchg是非原子性)因此在第二次比较的时候其他线程无法改变该部分内存值。

该方法执行的顺序如下图所示：

<img src="C:\Users\there\AppData\Roaming\Typora\typora-user-images\image-20200531154510146.png" alt="image-20200531154510146" style="zoom:50%;" />

ABA问题的话有影响就采用版本号的解决方法，没影响就不管。



## 2 synchronized

- 对象在内存中布局

<img src="C:\Users\there\AppData\Roaming\Typora\typora-user-images\image-20200531191042162.png" alt="image-20200531191042162" style="zoom:50%;" />

markword 8个字节

class pointer 4个字节

<img src="C:\Users\there\AppData\Roaming\Typora\typora-user-images\image-20200531194117750.png" alt="image-20200531194117750" style="zoom:50%;" />

- 锁升级过程

new（无锁） - 偏向锁 - 轻量级锁 - 重量级锁

下图是markword的组成

里面主要包含锁状态和分代年龄信息 

![image-20200531201529782](C:\Users\there\AppData\Roaming\Typora\typora-user-images\image-20200531201529782.png)



### volatile

缓存一致性协议MESI

CPU底层缓存行对齐 64k一行

**系统底层如何保证有序性**

内存屏障
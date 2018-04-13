# CAS
在JVM中的CAS操作就是基于处理器的CMPXCHG汇编指令实现的，因此，JVM中的CAS的原子性是处理器保障的

# ABA问题
ABA问题是指在CAS操作时，其他线程将变量值A改为了B，但是又被改回了A，等到本线程使用期望值A与当前变量进行比较时，发现变量A没有变，于是CAS就将A值进行了交换操作，但是实际上该值已经被其他线程改变过，这与乐观锁的设计思想不符合。ABA问题的解决思路是，每次变量更新的时候把变量的版本号加1，那么A-B-A就会变成A1-B2-A3，只要变量被某一线程修改过，改变量对应的版本号就会发生递增变化，从而解决了ABA问题。在JDK的java.util.concurrent.atomic包中提供了AtomicStampedReference来解决ABA问题，该类的compareAndSet是该类的核心方法，实现如下：

```java

```
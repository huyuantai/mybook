# CAS
在JVM中的CAS操作就是基于处理器的CMPXCHG汇编指令实现的，因此，JVM中的CAS的原子性是处理器保障的

# ABA问题与解决
ABA问题是指在CAS操作时，其他线程将变量值A改为了B，但是又被改回了A，等到本线程使用期望值A与当前变量进行比较时，发现变量A没有变，于是CAS就将A值进行了交换操作，但是实际上该值已经被其他线程改变过，这与乐观锁的设计思想不符合。ABA问题的解决思路是，每次变量更新的时候把变量的版本号加1，那么A-B-A就会变成A1-B2-A3，只要变量被某一线程修改过，改变量对应的版本号就会发生递增变化，从而解决了ABA问题。在JDK的java.util.concurrent.atomic包中提供了AtomicStampedReference来解决ABA问题，该类的compareAndSet是该类的核心方法，实现如下：

```java
public boolean compareAndSet(V   expectedReference,
                            V   newReference,
                            int expectedStamp,
                            int newStamp) {
   Pair<V> current = pair;
   return
       expectedReference == current.reference &&
       expectedStamp == current.stamp &&
       ((newReference == current.reference &&
         newStamp == current.stamp) ||
        casPair(current, Pair.of(newReference, newStamp)));
}  
```
我们可以发现，该类检查了当前引用与当前标志是否与预期相同，如果全部相等，才会以原子方式将该引用和该标志的值设为新的更新值，这样CAS操作中的比较就不依赖于变量的值了

# ABA问题对程序的影响
库存操作，出现ABA问题并不会对业务产生影响

再看一个堆栈操作会影响的例子：


并发1（上）：读取栈顶的元素为“A1”


并发2：进行了2次出栈

并发3：又进行了1次出栈

并发1（下）：实施CAS乐观锁，发现栈顶还是“A1”，于是修改为A2

此时会出现

系统错误

，因为此“A1”非彼“A1”
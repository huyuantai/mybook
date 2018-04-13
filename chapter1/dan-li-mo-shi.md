# 饿汉单例
类初始化就实例化，不管用不用到，天生线程安全（jvm保证）
不足：不能延迟初始化，不管实例用不用到，类初始化就实例化了
```java
//饿汉式单例类.在类初始化时，已经自行实例化   
public class Singleton1 {  
    private Singleton1() {}  
    private static final Singleton1 single = new Singleton1();  
    //静态工厂方法   
    public static Singleton1 getInstance() {  
        return single;  
    }  
}
```
# 懒汉单例，线程安全
延迟实例化，同步synchronized线程安全
不足：效率低，不同线程阻塞
```java
public class Singleton {  
    private static Singleton instance;  
    private Singleton (){}  
    public static synchronized Singleton getInstance() {  
    if (instance == null) {  
        instance = new Singleton();  
    }  
    return instance;  
    }  
}
```
# 静态内部类
jvm加载Singleton，不会实例化单例类；当getInstance()被调用时，才会加载SingletonHolder，实例化INSTANCE
优点：实现延迟实例化，又没用synchronized（懒汉 和 饿汉结合）

```java
public class Singleton {  
    private static class SingletonHolder {  
    private static final Singleton INSTANCE = new Singleton();  
    }  
    private Singleton (){}  
    public static final Singleton getInstance() {  
    return SingletonHolder.INSTANCE;  
    }  
}
```

# 枚举（特殊方式）
```java
public enum Singleton {  
    INSTANCE;  
    public void whateverMethod() {  
    }  
} 
```

# 双重校验锁
双层校验, 第一次校验不是线程安全的，也就是说可能有多个线程同时得到singleton为null的结果，接下来的同步代码块保证了同一时间只有一个线程进入，而第一个进入的线程会创建对象，等其他线程再进入时对象已创建就不会继续创建。这是一个很巧妙的方式，如果对整个方法同步，所有获取单例的线程都要排队，
只需要对创建过程同步来保证"单例"，多个线程不管是否已经有单例可以同时去请求
```java
public class Singleton {  
    private volatile static Singleton singleton;  
    private Singleton (){}  
    public static Singleton getSingleton() {  
    if (singleton == null) {  
        synchronized (Singleton.class) {  
        if (singleton == null) {  
            singleton = new Singleton();  
        }  
        }  
    }  
    return singleton;  
    }  
} 
```

# 双重校验锁为什么要加volatile
instance=new Singleton() 创建对象分为以下步骤：

> memory = allocate();　　// 1：分配对象的内存空间
> ctorInstance(memory);　// 2：初始化对象
> instance = memory;　　 // 3：设置instance指向刚分配的内存地址


在上面这行代码中，没有使用volatile关键字，的确即使发生了指令重排序，在同步代码块结束时，instance会被正确的初始化。

但是，假如你在其他线程中使用了这个static instance的静态变量，用instance==null的方法判断instance有没有被正确初始化的话，有可能会出现instance访问失败的情况。

在这个时间点上，同步代码块尚未执行完毕，由于指令重排序，instance对象已经指向分配的内存空间，但是instance尚未初始化完毕。在这时调用instance，会引发jvm的exception


# 防止反射漏洞
在构造函数里抛出异常

```java
private Singleton() {  
    if (null != instance) {  
        throw new RuntimeException();  
    }  
}  
```
# 防止反序列化漏洞
```java
private Object readResolve() throws ObjectStreamException {  
    return instance;  
}  
```




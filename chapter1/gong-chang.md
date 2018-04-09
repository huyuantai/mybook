# 简单工厂

![](/assets/simpleFactory.PNG)

```java
public class Client {
    public static void main(String[] args) {
        SimpleFactory simpleFactory = new SimpleFactory();
        Product product = simpleFactory.createProduct(1);
    }
}
```

```java
public class SimpleFactory {
    public Product createProduct(int type) {
        if (type == 1) {
            return new ConcreteProduct1();
        } else if (type == 2) {
            return new ConcreteProduct2();
        }
        return new ConcreteProduct();
    }
}
```

```java
public interface Product {
}
```

```java
public class ConcreteProduct implements Product{
}
```

```java
public class ConcreteProduct1 implements Product{
}
```

```java
public class ConcreteProduct2 implements Product{
}
```







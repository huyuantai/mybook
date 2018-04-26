# String 可以被继承吗？
> 不可以。因为String类被final所修饰，故不能被继承

# 在java中，对于不管是基本类型还是引用类型，采用的都是值调用

```java
public static void main(String[] args) {  
    String x = new String("ab");  
    change(x);  
    System.out.println(x);  
}  
   
public static void change(String x) {  
    x = "cd";  
}
```
输出为原来的“ab”！

![](/assets/20131130101801156.jpg)


```java
public class StringBufferDemo {
    public static void main(String[] args) {
    
        String s1 = "hello";
        String s2 = "world";
        System.out.println(s1 + "---" + s2);// hello---world
        change(s1, s2);
        System.out.println(s1 + "---" + s2);// hello---world



        StringBuffer sb1 = new StringBuffer("hello");
        StringBuffer sb2 = new StringBuffer("world");
        
        System.out.println(sb1 + "---" + sb2);// hello---world
        change(sb1, sb2);
        System.out.println(sb1 + "---" + sb2);// hello---worldworld

    }

    public static void change(StringBuffer sb1, StringBuffer sb2) {
        sb1 = sb2;
        sb2.append(sb1);
    }

    public static void change(String s1, String s2) {
        s1 = s2;
        s2 = s1 + s2;
    }
}
```

# 总结
> String 传递时，无论s1 = s2;s2 = s1 + s2;都不影响原来的s1，s2
StringBuffer 传递时，sb1 = sb2;不影响原来的s1，s2
 sb2.append(sb1); 会影响，由于前面有sb1 = sb2，所以这里的输出为worldworld

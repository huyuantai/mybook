# String 可以被继承吗？
> 不可以。因为String类被final所修饰，故不能被继承

# 在java中，对于不管是基本类型还是引用类型，采用的都是值调用

public static void main(String[] args) {  
    String x = new String("ab");  
    change(x);  
    System.out.println(x);  
}  
   
public static void change(String x) {  
    x = "cd";  
}
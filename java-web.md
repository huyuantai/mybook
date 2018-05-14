# Servlet的生命周期

Servlet的生命周期分为5个阶段：加载、创建、初始化、处理客户请求、卸载。

(1)加载：web容器通过类加载器使用servlet类对应的文件加载servlet

(2)创建：通过调用servlet构造函数创建一个servlet对象

(3)初始化：调用init方法初始化,servlet一生只会调用该方法一次

(4)处理客户请求：当浏览器访问Servlet的时候，Servlet 会调用service()方法处理请求，由service()来交由相应的doPost或doGet方法处理

(5)卸载：调用destroy方法让servlet自己释放其占用的资源


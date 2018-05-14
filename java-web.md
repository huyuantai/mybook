# Servlet的生命周期

Servlet的生命周期分为5个阶段：加载、创建、初始化、处理客户请求、卸载。

(1)加载：web容器通过类加载器使用servlet类对应的文件加载servlet

(2)创建：通过调用servlet构造函数创建一个servlet对象

(3)初始化：调用init方法初始化,servlet一生只会调用该方法一次

(4)处理客户请求：当浏览器访问Servlet的时候，Servlet 会调用service()方法处理请求，由service()来交由相应的doPost或doGet方法处理

(5)销毁：调用destroy方法让servlet自己释放其占用的资源,一个Servlet如果长时间不被使用的话，也会被Tomcat自动销毁

(60卸载:当Servlet调用完destroy()方法后，等待垃圾回收。如果有需要再次使用这个Servlet，会重新调用init()方法进行初始化操作

> sevlet的生命周期中，servlet的初始化和销毁只会发生一次，
因此init()和destroy（）方法只能被servlet容器调用一次，
service()方法取决与servlet被客户端访问的次数
destroy()方法仅执行一次，即在服务器停止且卸载Servlet时执行该方法

# forward和redirect的区别
实际发生位置不同，地址栏不同

转发是发生在服务器的

转发是由服务器进行跳转的，细心的朋友会发现，在转发的时候，浏览器的地址栏是没有发生变化的，在我访问Servlet111的时候，即使跳转到了Servlet222的页面，浏览器的地址还是Servlet111的。也就是说浏览器是不知道该跳转的动作，转发是对浏览器透明的。通过上面的转发时序图我们也可以发现，实现转发只是一次的http请求，一次转发中request和response对象都是同一个。这也解释了，为什么可以使用request作为域对象进行Servlet之间的通讯。


重定向是发生在浏览器的

重定向是由浏览器进行跳转的，进行重定向跳转的时候，浏览器的地址会发生变化的。曾经介绍过：实现重定向的原理是由response的状态码和Location头组合而实现的。这是由浏览器进行的页面跳转实现重定向会发出两个http请求，request域对象是无效的，因为它不是同一个request对象

用法不同:

很多人都搞不清楚转发和重定向的时候，资源地址究竟怎么写。有的时候要把应用名写上，有的时候不用把应用名写上。很容易把人搞晕。记住一个原则： 给服务器用的直接从资源名开始写，给浏览器用的要把应用名写上

request.getRequestDispatcher("/资源名 URI").forward(request,response)

转发时"/"代表的是本应用程序的根目录【zhongfucheng】
response.send("/web应用/资源名 URI");
重定向时"/"代表的是webapps目录

能够去往的URL的范围不一样:
转发是服务器跳转只能去往当前web应用的资源
重定向是服务器跳转，可以去往任何的资源

传递数据的类型不同
转发的request对象可以传递各种类型的数据，包括对象
重定向只能传递字符串


跳转的时间不同
转发时：执行到跳转语句时就会立刻跳转
重定向：整个页面执行完之后才执行跳转


# 过滤器和拦截器的区别

1、拦截器是基于java的反射机制的，而过滤器是基于函数回调

2、过滤器依赖于servlet容器，而拦截器不依赖于servlet容器

3、拦截器只能对action请求起作用，而过滤器则可以对几乎所有的请求起作用

4、拦截器可以访问action上下文、值栈里的对象，而过滤器不能

5、在action的生命周期中，拦截器可以多次被调用，而过滤器只在容器初始化时调用一次

拦截器 ：是在面向切面编程的就是在你的service或者一个方法，前调用一个方法，或者在方法后调用一个方法比如动态代理就是拦截器的简单实现，在你调用方法前打印出字符串（或者做其它业务逻辑的操作），也可以在你调用方法后打印出字符串，甚至在你抛出异常的时候做业务逻辑的操作。

过滤器：是在JavaWeb中，你传入的request,response提前过滤掉一些信息，或者提前设置一些参数，然后再传入servlet或者struts的action进行业务逻辑，比如过滤掉非法url（不是login.do的地址请求，如果用户没有登陆都过滤掉）,或者在传入servlet或者struts的action前统一设置字符集，或者去除掉一些非法字符.


# 简单的谈一下SpringMVC的工作流程
流程 
1、用户发送请求至前端控制器DispatcherServlet 
2、DispatcherServlet收到请求调用HandlerMapping处理器映射器。 
3、处理器映射器找到具体的处理器，生成处理器对象及处理器拦截器(如果有则生成)一并返回给DispatcherServlet。 
4、DispatcherServlet调用HandlerAdapter处理器适配器 
5、HandlerAdapter经过适配调用具体的处理器(Controller，也叫后端控制器)。 
6、Controller执行完成返回ModelAndView 
7、HandlerAdapter将controller执行结果ModelAndView返回给DispatcherServlet 
8、DispatcherServlet将ModelAndView传给ViewReslover视图解析器 
9、ViewReslover解析后返回具体View 
10、DispatcherServlet根据View进行渲染视图（即将模型数据填充至视图中）。 
11、DispatcherServlet响应用户

![](/assets/799093-20160724233025857-1256444961.jpg)




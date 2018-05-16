# Servlet相关类的关系
![](/assets/20140926001639734.png)



# Servlet对象的创建时机：用户请求之时或应用启动之时。

1.客户端第一次请求某个Servlet时，容器创建该Servlet实例，这也是大部分Servlet创建实例的时机； 
2.Web应用启动时立即创建Servlet实例，即 load-on-startup Servlet

> load-on-servlet 指的是应用启动时就创建的Servlet，这些Servlet通常是用于后台服务的Servlet或者需要拦截很多请求的Servlet

# Servlet的执行流程如下图所示：
 
 (1) User Agent 向 Servlet容器（Tomcat）发出Http请求； 
　　
(2) Servle容器接收 User Agent 发来的请求； 
　　
(3) Servle容器根据web.xml文件中Servlet相关配置信息，将请求转发到相应的Servlet； 
　　
(4) Servlet容器创建一个 HttpServlet对象，用于处理请求； 
　　
(5) Servlet容器创建一个 HttpServletRequest对象，将请求信息封装到这个对象中； 
　　
(6) Servlet容器创建一个HttpServletResponse对象； 
　　
(7) Servlet容器调用HttpServlet对象的service方法，并把HttpServltRequest对象与HttpServltResponse对象作为参数传给 HttpServlet 对象； 
　　
(8) HttpServlet调用HttpServletRequest对象的有关方法，获取Http请求信息； 
　　
(9) HttpServlet调用JavaBean对象（业务逻辑组件）处理Http请求； 
　　
(10) HttpServlet调用HttpServletResponse对象的有关方法，生成响应数据； 
　　
(11) Servlet容器将HttpServlet的响应结果传给 User Agent
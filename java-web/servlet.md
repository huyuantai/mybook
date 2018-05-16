# Servlet对象的创建时机：用户请求之时或应用启动之时。

1.客户端第一次请求某个Servlet时，容器创建该Servlet实例，这也是大部分Servlet创建实例的时机； 
2.Web应用启动时立即创建Servlet实例，即 load-on-startup Servlet
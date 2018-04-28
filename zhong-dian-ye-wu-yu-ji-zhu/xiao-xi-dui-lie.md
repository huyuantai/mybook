# 消息队列问题
* 消息丢失
* 消息确认
* 消息持久化
* 消息堆积
* 消息重复重发与顺序消息
* 高可用


# 没有消息确认，消息会丢失
发送者没法确认是否发送成功,消费者处理失败也无法反馈


# rabbimq
rabbitmq-plugins enable rabbitmq_management 
访问地址：http://ip:15672 / localhost:15672
默认用户名：guest （只能localhost登陆） 
默认密码：guest 


# 消息队列问题
* 消息丢失
* 消息确认
* 消息持久化
* 消息堆积
* 消息重复重发与顺序消息
* 高可用
* 消息拒绝


# 没有消息确认，消息会丢失
发送者没法确认是否发送成功,消费者处理失败也无法反馈


# 消息重复堆积
如果抛异常或unack（并且requeue为true），消息会一直重新入队列，一不小心就会xxxxx一大堆消息不断重复

# rabbimq
rabbitmq-plugins enable rabbitmq_management 
访问地址：http://ip:15672 /   http://localhost:15672
默认用户名：guest （只能localhost登陆） 
默认密码：guest 


# rabbitmq confirm、return
#### 发送消息确认

如果消息没有到exchange,则confirm回调,ack=false

如果消息到达exchange,则confirm回调,ack=true

exchange到queue成功,则不回调return

exchange到queue失败,则回调return(需设置mandatory=true,否则不回回调,消息就丢了)


备注:需要说明,spring-rabbit和原生的rabbit-client ,表现是不一样的.

测试的时候,原生的client,exchange错误的话,直接就报错了,是不会到confirmListener和returnListener的

pring对rabbitmq支持的一些示例,主要包括: 发送消息确认 消费消息确认 死信队列

# Dead Letter 本来不是用于延时发送的, 而是处理 消息过期,消息被拒绝,队列超出限制大小

Dead Letter 会转发到普通的队列


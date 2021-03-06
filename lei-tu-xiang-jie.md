# 记忆思路
* 关系分为：纵向、横向
##### 纵向
> 纵向是空心三角形，记忆思路（纵的人字与三角线类似，形状相近记忆）

> 纵向是继承、泛化，继承是实现，泛化是虚线，记忆思路（泛化的泛字三点水与虚线类似，形状相近记忆）

##### 横向
> 横向是箭头，棱形
> 纵向是关联依赖、组合聚合，记忆思路（组合聚合的合字的口与棱形类型，形状相近记忆）

关联：成员变量
依赖：1.局部变量 2.类构造方法或类方法的传入参数 2.静态方法的调用

组合：整体与部分关系，不可分割 记忆思路（娱乐圈组合是不能分割单飞，组合分割就散了）

聚合：整体与部分关系，可分割， 记忆思路 聚会，有聚有散
组合聚合：成员变量

--------------

* 耦合强弱比较：依赖< 关联< 聚合< 组合< 继承
* 提倡不用继承，使用组合！！


* 依赖关联箭头形
* 关联细分[聚合组合]菱形
* 继承实现空心三角形


* 依赖虚线箭头 全局、方法局部变量、方法参数或返回值
* 关联聚合组合 成员变量，聚合构造函数参数传递，组合构造函数直接new实例化
* 继承实现父类、父接口










# 继承关系（泛化与实现）——空心三角形

> ![](/assets/jicheng.png)： 继承抽象类、实现接口

------

> ![](/assets/fanhua.png)：继承具体类（即非抽象类）


# 关联依赖关系——小箭头
> ![](/assets/guanlian.png)：关联关系
【代码体现】：成员变量

------

> ![](/assets/yilai.png)依赖关系
临时性，杜绝双向依赖，依赖还“使用”对方的方法与属性
>【代码体现】：
>1.局部变量
>2.类构造方法或类方法的传入参数
>2.静态方法的调用



# 组合聚合关系——菱形 整体与部分
> ![](/assets/zuhe.png)：组合关系
整体与部分，一对多；
强依赖，整体不存在，部分就不存在 
【代码体现】：成员变量

------

> ![](/assets/juhe.png)：聚合关系
>整体与部分，一对多；
>弱依赖，整体不存在，部分仍可存在 
>【代码体现】：成员变量

https://blog.csdn.net/lfsf802/article/details/8987267

耦合强弱比较：依赖< 关联< 聚合< 组合< 继承

提倡不用继承，使用组合！！

![](/assets/uml.png)







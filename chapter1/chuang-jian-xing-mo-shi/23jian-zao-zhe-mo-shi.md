# 定义
将一个复杂对象的构建与它的表示分离，使得同样的构建过程可以创建不同的表示

# 主要作用
在用户不知道对象的建造过程和细节的情况下就可以直接创建复杂的对象。

> 用户只需要给出指定复杂对象的类型和内容；
建造者模式负责按顺序创建复杂对象（把内部的建造过程和细节隐藏起来)

# 解决的问题
方便用户创建复杂的对象（不需要知道实现过程）
代码复用性 & 封装性（将对象构建过程和细节进行封装 & 复用）
> 例子：造汽车 & 买汽车。
工厂（建造者模式）：负责制造汽车（组装过程和细节在工厂内）
汽车购买者（用户）：你只需要说出你需要的型号（对象的类型和内容），然后直接购买就可以使用了
（不需要知道汽车是怎么组装的（车轮、车门、发动机、方向盘等等））

# 优点
易于解耦
将产品本身与产品创建过程进行解耦，可以使用相同的创建过程来得到不同的产品。也就说细节依赖抽象。

易于精确控制对象的创建
将复杂产品的创建步骤分解在不同的方法中，使得创建过程更加清晰

易于拓展
增加新的具体建造者无需修改原有类库的代码，易于拓展，符合“开闭原则“。

# 缺点
建造者模式所创建的产品一般具有较多的共同点，其组成部分相似；如果产品之间的差异性很大，则不适合使用建造者模式，因此其使用范围受到一定的限制。
如果产品的内部变化复杂，可能会导致需要定义很多具体建造者类来实现这种变化，导致系统变得很庞大。

# 应用场景
需要生成的产品对象有复杂的内部结构，这些产品对象具备共性；
隔离复杂对象的创建和使用，并使得相同的创建过程可以创建不同的产品

# 示例

#### Client
```java
public class Client
{
	public static void main(String args[])
	{
	    
	    MealBuilder mb= new SubMealBuilderB();
		//服务员是指挥者
		KFCWaiter waiter=new KFCWaiter();
	    //服务员准备套餐
	    waiter.setMealBuilder(mb);
	    //客户获得套餐
	    Meal meal=waiter.construct();
        
        System.out.println("套餐组成：");
        System.out.println(meal.getFood());
        System.out.println(meal.getDrink());
	}
}
```

# MealBuilder
```java
public abstract class MealBuilder
{
	protected Meal meal=new Meal();
	public abstract void buildFood();
	public abstract void buildDrink();
	public Meal getMeal()
	{
		return meal;
	}
}
```

# SubMealBuilderA
```java
public class SubMealBuilderA extends MealBuilder
{
	public void buildFood()
	{
		meal.setFood("一个鸡腿堡");
	}
	public void buildDrink()
	{
	    meal.setDrink("一杯可乐");
	}
}
```

# SubMealBuilderB
```java
public class SubMealBuilderB extends MealBuilder
{
	public void buildFood()
	{
		meal.setFood("一个鸡肉卷");
	}
	public void buildDrink()
	{
		 meal.setDrink("一杯果汁");
	}
}
```

































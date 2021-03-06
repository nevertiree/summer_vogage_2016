# 07月17日

##关键词

静态工厂方法

##1.静态工厂方法

###1.静态工厂方法的概念和定义

>创建类的实例的常见方式是用new语句调用类的构造方法。这种情况下，程序可以创建任意多个实例，每执行一条new语句，都会导致Java虚拟机的堆区中产生一个新的对象。类也可以提供静态工厂方法，它只是一个返回类的实例的静态方法。

###2.静态工厂方法的实现



###3.静态工厂方法的优点

1.有不受限制的方法名字

构造方法的名字必须与类名相同。

这一特性的优点是符合Java语言的规范，缺点是类的所有重载的构造方法的名字都相同，不能从名字上区分每个重载方法，容易引起混淆。静态工厂方法的方法名可以是任意的，这一特性的优点是可以提高程序代码的可读性，在方法名中能体现与实例有关的信息。

对于不同的工厂方法可以采用不同的会意的名字，是程序具有更好的可读性。通过不同的名字产生特定的对象。 

2.不必每次调用它们的时候都创建一个新的对象

3.可以返回原返回类型的任何子类型的对象

至于产生什么类型的对象没有限制，这就意味这只要返回原返回类型或原返回类型的子类型都可以，这样就加大了程序设计和使用的灵活行

>这一特性可以在创建松耦合的系统接口时发挥作用

4.在创建参数化实例的时候，代码会更加简洁

5.静态工厂方法所创建的对象可以在编译时不存在

>静态工厂方法采用反射动态创建对象，（类似spring的IOC容器方转）。最典型的例子就是Spring服务提供者框架，Service Provider Iframe是一种用于在运行时刻产生对象的框架，达到对象的创建与使用分离，是对象的客户和对象之间解耦，增加程序的灵活性和可扩展性。

###4.静态工厂方法的缺点

1.类如果不含公有或者受保护的构造器，就不能被子类化

>如果将要创建的对象的构造方法是私有的或是default的，就有可能不能创建该对象。 

2.与其他的静态方法没有任何区别

静态工厂方法与别的静态方法没有区别，只不过该方法产生的类对象。用户难以识别类中到底哪些静态方法专门负责返回类的实例。目前比较流行的规范是把静态工厂方法命名为valueOf或者getInstance。 

valueOf：该方法返回的实例与它的参数具有同样的值，例如： 
Integer a=Integer.valueOf(100); //返回取值为100的Integer对象 
从上面代码可以看出，valueOf()方法能执行类型转换操作，在本例中，把int类型的基本数据转换为Integer对象。 

getInstance：返回的实例与参数匹配，例如： 
//返回符合中国标准的日历 
Calendar cal=Calendar.getInstance(Locale.CHINA); 




例如Class实例是Java虚拟机在加载一个类时自动创建的，程序无法用new语句创建java.lang.Class类的实例，因为Class类没有提供public类型的构造方法。为了使程序能获得代表某个类的Class实例，在Class类中提供了静态工厂方法forName(String name)，它的使用方式如下：

`java

Class c=Class.forName("Sample"); //返回代表Sample类的实例

`

静态工厂方法最主要的特点是：每次被调用的时候，不一定要创建一个新的对象

静态工厂方法可用来创建以下类的实例。 
单例类：只有惟一的实例的类。 
枚举类：实例的数量有限的类。 
具有实例缓存的类：能把已经创建的实例暂且存放在缓存中的类。 
具有实例缓存的不可变类：不可变类的实例一旦创建，其属性值就不会被改变。

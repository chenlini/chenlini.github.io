---
layout: post
title: "抽象类和接口"
date: 2017-06-12 17:31:48 +0800
comments: true
categories: java
---
#java基础知识--抽象类和接口的区别

##1. 抽象类
抽象类就是为了实现面向对象设计的，因此必然是为了能够被继承。
>1）抽象方法默认为public。可以是protected，但是不能是private。
>
>2）抽象类不能直接创建一个对象；

>3）子类必须实现父类所有的抽象方法。否则的话必须定义该子类也是抽象类。
>
>4)抽象类中也可以有不是abstract的成员方法和数据成员。
>
```
abstract class Class1 {
    abstract void method();
}
```

##2.接口

接口同样是为了实现面向对象而设计的。但是接口中的数据成员都是默认为public static final的,但是一般不会定义数据成员，而所有的成员函数都是public abstract的。

```
interface interface1{
    void method();
}
```
##两者区别

>1. 抽象类可以多种类型的数据成员以及成员函数，因此抽象类可以定义一些默认的行为。接口只能有abstract的函数以及public static final的数据成员。
2. 一个类只能继承自一个对象，但是可以实现多个接口。
3. 设计理念：其实abstract class表示的是"is-a"关系，interface表示的是"like-a"关系。 要明确设计理念，该类的本质是什么，实现了哪些方法。可以查找AlarmDoor的例子。
4. 注意接口的数据成员必须赋予初始值，使得实现的类无法改变该值。抽象类中的数据成员默认为friendly类型。 



参考资料：
http://www.cnblogs.com/beanmoon/archive/2012/12/06/2805221.html
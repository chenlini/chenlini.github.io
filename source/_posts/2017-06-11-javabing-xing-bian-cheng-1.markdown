---
layout: post
title: "java并行编程(1)"
date: 2017-06-11 21:15:14 +0800
comments: true
categories: java
---
#Java并行编程（1）实现多线程的方法
###简单基础知识：
java的并发编程一定要考虑四个方面的内容。
>1. 共享性：当多个线程共享一份数据的时候就会有数据的安全问题。
>
>2. 互斥性：最基本的就是需要保证数据在同一时间只被一个线程锁修改。
>
>3. 原子性：类似于数据库的一致性，在数据修改到一半的时候，又被其他的操作修改。
>
>4. 可见性：比如线程1对数据进行了修改，但是还没有同步到最终版本，因此线程2对这次就该就是不可见的，会出现问题。
>
>5. 有序性:编译器会对代码做重排序的操作，这种排序有可能遵照原始线程的代码顺序，也可能是无序的优化，会有线程不安全的问题。
<!--more-->
java中主要有以下几种实现多线程的方法：

1. 继承Thread类

```
class Mytest extends Thread{
    private int num = 8;
    public void run(){
        for (int i=0;i<4;i++)
        {
            if(num > 0){
                System.out.print(num);num--;
            }
        }
    }
}
public class javatest {

    public static void main(String args[]) {
        new Mytest().start();
        new Mytest().start();
        new Mytest().start();
    }
}
```

输出的是：876587658765
这里new了三个Thread对象，每个对象是互不干扰的，因此相当于做了三遍操作。


2. 实现Runnable接口

```
class Mytest  implements Runnable{
    private int num = 8;
    public void run(){
        for (int i=0;i<10;i++)
        {
            if(num > 0){
               System.out.print(num);num--;            }
        }
    }
}
public class javatest {

    public static void main(String args[]) {
        Mytest test=new Mytest();
        new Thread(test).start();
        new Thread(test).start();
    }
}


```
输出的是：87654321
这里同样new了两个Thread，但是它们操作的是一个Runnable对象，虽然这里顺序是对的，但是是有可能出现86754312的情况的。这里就需要用到下一节讲到的同步方法：synchronized

3. 匿名的多线程方法：

```
lass Mytest  {
    private int num = 8;
    public void method(){
        for (int i=0;i<4;i++)
        {
            if(num > 0){
                System.out.print(num);num--;
            }
        }
    }
}
public class javatest {

    public static void main(String args[]) {
        Mytest test =new Mytest();
        new Thread(new Runnable() {
            public void run() {
                test.method();
            }
        }).start();
        new Thread(new Runnable() {
            public void run() {
                test.method();
            }
        }).start();
    }
}
```
方法3的作用和方法2是一样的，只不过是匿名的线程，同时也更加灵活，可以让每个线程执行不同的内容。方法3还可以改成lambda的形式：

```
public static void main(String args[]) {
        Mytest test =new Mytest();
        new Thread(() -> {
            test.method();
        }).start();
        new Thread(() -> {
            test.method();
        }).start();
    }
```





参考材料：
http://www.cnblogs.com/paddix/p/5374810.html
http://blog.csdn.net/ns_code/article/details/17161237
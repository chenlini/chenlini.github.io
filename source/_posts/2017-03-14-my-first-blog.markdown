---
layout: post
title: "C++中static和const"
date: 2017-03-15 15:14:26 +0800
comments: true
categories: language
---



static是静态常量，const是指类的内部是静态的。
const定义的常量在超出其作用域之后其空间会被释放，而static定义的静态常量在函数执行后不会释放其存储空间。

<!--more-->

1. static静态成员变量不能在类的内部初始化。

2. const成员变量也不能在类定义处初始化，只能通过构造函数初始化列表进行，并且必须有构造函数。
3. const修饰指针变量时：

　　(1)只有一个const，如果const位于*左侧，表示指针所指数据是常量，不能通过解引用修改该数据；指针本身是变量，可以指向其他的内存单元。

　　(2)只有一个const，如果const位于*右侧，表示指针本身是常量，不能指向其他内存地址；指针所指的数据可以通过解引用修改。

　　(3)两个const，*左右各一个，表示指针和指针所指数据都不能修改。

3. cosnt成员函数主要目的是防止成员函数修改对象的内容。即const成员函数不能修改成员变量的值，但可以访问成员变量。const成员函数不能调用非const成员函数，因为非const成员函数可以会修改成员变量

4. static成员函数主要目的是作为类作用域的全局函数。不能访问类的非静态数据成员。类的静态成员函数没有this指针，这导致：1、不能直接存取类的非静态成员变量，调用非静态成员函数2、不能被声明为const、volatile
5. const static 的成员也只能在外部初始化，而且不带static字样。

```cpp
        using namespace std;  
        class A  
        {  
        public:  
            A(int a);  
            static void print();//静态成员函数  
        private:  
        static int aa;//静态数据成员的声明  
        static const int count;//常量静态数据成员（可以在构造函数中初始化）  
         const int bb;//常量数据成员  
        };  
        int A::aa=0;//静态成员的定义+初始化  
        const int A::count=25;//静态常量成员定义+初始化  
        A::A(int a):bb(a)//常量成员的初始化  
        {  
             aa+=1;  
        }  
        void A::print()  
        {  
              cout<<"count="<<count<<endl;  
              cout<<"aa="<<aa<<endl;  
        }  
        #endif  
        void main()  
        {  
            A a(10);  
            A::print();//通过类访问静态成员函数  
            a.print();//通过对象访问静态成员函数  
        }  
```

        

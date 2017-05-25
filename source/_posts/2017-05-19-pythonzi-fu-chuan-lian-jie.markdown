---
layout: post
title: "python字符串连接"
date: 2017-05-19 11:14:50 +0800
comments: true
categories: python
---
##python字符串连接

python有若干种字符连接方式，找找资料总结如下：

1. ‘+’号方法

        str1='aaa'
        str2='bbb'
        print(str1 + str2)
        'aaabbb'
    

2. ‘,’号方法，会有空格。

        str1='aaa'
        str2='bbb'
        print(str1 , str2)
        'aaa bbb'

3. 空格连接

        str1='aaa'
        str2='bbb'
        print(str1 str2)
        'aaabbb'
    
4. ‘%’连接

        str1='aaa'
        str2='bbb'
        print("%s,%s"%(str1,str2))
        'aaa,bbb'
    
5. join
    
        str=['aaa','bbb','ccc']
        t=','
        print(t.join(str))
        'aaa,bbb,ccc'
    
6. '*'连接

        a = 'abc'
        a * 3 = 'abcabcabc'
---
layout: post
title: "hive优化"
date: 2017-05-13 00:12:34 +0800
comments: true
categories: Hive
---

##Hive 语句简单优化

使用Hive的过程中，因为数据倾斜的问题可能会造成效率十分地下，以下记录一些hive的简单语句的优化操作。大部分都来自网络，查资料的时候看到就顺便记录一下。



###1. 设置

```sql
set Hive.groupby.skewindata=true;
#解决jion造成的倾斜
set Hive.optimize.skewjoin = true;
```

###2. 简单统计语句

```sql
#优化前：
select count(distinct id) from table A;
#优化后
select count(*) from (select distinct id from tableA)t;
```

###3. 列转行

```sql
#建表
    create table A(
    colume1 string,
    colume2s array<string>
    )ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' ; 
COLLECTION ITEMS TERMINATED BY ',' ;
#插入数据，B是原始表格，按照colume1插入数据
insert  overwrite  table  A  
select max(B.colume1),  collect_set(B.colume2)  as colume2s from B group by B.colume1;

方法2:
create table A as select max(B.colume1),concat_ws(',',collect_set(B.colume2)) as colume2s from B group by B.colume1;
```

###4. 多列的distinct

```sql
#优化前 
select t1， count(distinct t2) as t3 from A group by t1;  
#优化后 
select t1， count(*) as t3  
from (select distinct t1， t2 from A) group by t1; 
```

###5. 查询的时候还可以通过并行来进行优化

```sql
set Hive.exec.parallel=true;
#默认是8
set Hive.exec.parallel. thread.number=n;
select * from   
(  
select count(t1) from A   
where y = 2017 and m = 1  
union all   
select count(t1) from A   
where y = 2017 and m = 2  
union all   
select count(t1) from A   
where y = 2017 and m = 3  
)t 
```      
  
###6. 减少Job数量

优化实现思路，减少job的数量。
举例，统计购买既物品A又购买物品B的用户的数量。
优化前：

```sql

select count(*) 
from
(select distinct user 
from T1 where item = ‘A’) A
join 
(select distinct user 
from T1 where item = ‘B’) B 
on A.user = B.user;

```

优化后：

```sql
select count(*) 
from T1 group by user
having (count(case when item = ‘A’ then 1 end) > 0
    and count(case when item = ‘B’ then 1 end) > 0) 
```   
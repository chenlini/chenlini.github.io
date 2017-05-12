---
layout: post
title: "排序汇总"
date: 2017-03-15 22:12:55 +0800
comments: true
categories:  DataStructure
---

几种简单排序算法实现
<!--more-->
##简单选择排序
```cpp
         
    void simpleRank(vector<int> R){
            int s;
            for(int i=0;i<R.size();i++){
                s=0;
                for(int j=i+1;R.size();j++){
                    if(R[j]<R[s])s=j;
                }
                swap(R[i],R[s]);
            }
            
        }
```
        
时间复杂度O（n^2 ）,是不稳定的排序算法。空间复杂度为O（n）
##直接插入排序
```cpp
   void InsertRank(vector<int> R){
	
	   for(int i=1;i<R.size();i++){
		int tmp=R[i];
		int j=i;
		while(j>0&&tmp<R[j-1]){
			R[j]=R[j-1];j--;
		}
		R[j]=tmp;
	}
	
    }
    ```
当原始数据是有序的，直接插入排序最好的时间复杂度是O（n）最坏情况为O（n^2 ），是稳定的排序算法。空间复杂度为O（n）

##冒泡排序
```cpp
    void maopaoRank(vector<int> R){
	int j=R.size()-1;
		while(j>0){
			int last=0;
			for(int i=0;i<j;i++){
				if(R[i]>R[i+1]){swap(R[i],R[i+1]);
							last=i;}
			}
    		j=last;
		}
    }
```
注意并不是一定要进行R.size()趟，当没有交换的元素的时候就可以结束循环了。当原始数据是有序的，直接插入排序最好的时间复杂度是O（n）最坏情况为O（n^2 ），是稳定的排序算法。需要额外的栈资源。

##快速排序
```cpp
        //函数封装
        void QuickSort(vector<int> R){
	Quick(R,0,R.size()-1);
        }
        void Quick(vector<int> R, int left,int right){
	int i,j;
	if(left<right){//待排元素多于一个
		i=left;
		j=right+1;
		do{
			do i++;while(R[i]<R[left]);//寻找第一个大于R[left]的元素
			do j--;while(R[j]>R[left]);//寻找第一个小于R[left]的元素
			if(i<j)swap(R[i],R[j]);//交换元素，如果此时i>j久不用交换了
		}while(i<j);
		swap(R[left],R[j]);
		Quick(R,left,j-1);//低端
		Quick(R,j,right);//高端
	}}
```
快速排序有三种选择分割点的方法：

1. A[(left+right)/2]作为分割点，与第一个点交换
2. 取随机数与第一个点交换
3. 比较A[left],A[right],A[(left+right)/2]，取中间的和第一个点交换。

优化方法：先排短的子序列，再排长的子序列。

时间复杂度：平均情况O(nlogn)，最坏情况为O(n^2).快速排序是不稳定的排序算法。

##二路合并排序


```cpp
include<iostream>
using namespace std;
int * Merge(){
}

```

 

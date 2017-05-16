---
layout: post
title: "ruby升级"
date: 2017-05-14 23:21:38 +0800
comments: true
categories: ruby
---

##Mac升级系统后需要更新ruby
前段时间学学怎么用octopress写博客，更新了mac版本后就发现不能rake preview了，网上查了一下发现需要更新ruby，中间遇到了一些问题，记录如下：

之前没有通过rvm安装ruby，要更新比较麻烦，因此现在从新安装rvm.


    #安装rvm
    curl -L https://get.rvm.io | bash -s stable
    source ~/.bashrc
    source ~/.bash_profile
    #查看已知ruby版本
    rvm list know
    #安装版本
    rvm install 2.3.3



注意：在install的时候可能会出现错误，错误原因是brew需要update，因此需要执行以下语句

    brew update

如果brew update 出现错误，"The /usr/local directory is not writable." 需要去到/usr/local/目录下面执行：

    sudo chown -R $(whoami) /usr/local
    brew prune

这样就可以brew update了。

完成ruby的更新之后，发现还是不能rake preview,还是会报错！发现需要重新安装bundler

    gem install bundler

但是重新安装完了之后又又问题了，rake不见了！只能再走一遍。
    
    bundle install

#####补充rvm的命令

    rvm use 2.3.3
    #卸载
    rvm remote 2.3.3

    
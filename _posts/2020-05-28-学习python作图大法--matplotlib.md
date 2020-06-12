---
layout:     post
title:      学习python作图大法————matplotlib~
subtitle:   一个专门用来做高大上的图表的库~
date:       2020-05-28
author:     David
header-img: pict/FormentorHolidays.jpg
catalog: true
tags:
    - Blog
    - Life
    - Python
    - matplotlib 
---

# 前言

最近把论文弄完之后， 查重也过了，很爽，然后学了一下怎么从网站上爬必应的壁纸(虽然最后用的程序不是我写的但我可以读懂什么意思，怎么个原理了， 之后会在实践一下，然后再发到这里面来)，查重过了之后基本就剩下了答辩的PPT没弄了，当然最近还在纠结一件事就是，，要不要申请优秀论文。。

虽说咱这个可能跟大佬比没啥东西，但怎么说呢，也确实是努力过了（也偷懒很多当然。。），但感觉心里还是先尝试一下的。。  再看看吧

还有一件事就是，这段时间还看了一部英剧，Normal People， 把整部剧的资源下载下来了，打算也学学B站的大佬们弄一弄婚检~~~嘿嘿·~~  基础的Au Pr Ae什么的差不多都会 ，就只有转场当时没有学，到时候学学这个就好了~

然后今天我刷知乎，发现一门新的语言，有人说会在未来超越python。。 

我心想，这tm一个还没学通透呢， 又给我整一个。。 学不完啊也，，（毕竟我渣渣）

哪个语言的名字叫做Julia  说虽然是动态的语言，但是速度，效率都要高于python，很接近静态语言C和C++了

但我还具体没学过那两个  也不好说  但不管怎么样  

这都和我没关系。。。

（其实我还想学一学操作系统 数据结构的课，，感觉要学的好多呀）

# 正文

同学推荐了一个学习python的人  叫做  莫烦python  我这里要讲的matplotlib就是跟着这位哥哥学的

话不多说 开始了：

首先自然是安装了，Linux自然就是

    sudo pip3 install matplotlib

教程上面讲Windows上面的那个比较繁琐， 我记得当时我分明就直接cmd输入同样的pip install 命令就可以了

当然 一个Anoconda就可以解决

```
    import matplotlib.pyplot as plt
    import numpy as np

    x = np.linspace(-1,1,50)
    y = 2*x + 1
    plt.plot(x,y)
    plt.show()
```
 上面即为最简单的基本用法


```
    import matplotlib.pyplot as plt
    import numpy as np

    x = np.linspace(-3,3,50)
    y2 = 2*x + 1
    y1 = x**2

    plt.figure()
    plt.plot(x,y1)

    plt.figure(num=3,figsize=(8,5),color='red',linewidth=1.0,linestyle='--')
    plt.plot(x,y2)
    plt.plot(x,y1)

    plt.figure(num=3, figsize=(8, 5),)
    plt.plot(x, y2)
    plt.plot(x, y1, color='red', linewidth=1.0, linestyle='--')

    plt.xlim((-1,2))
    plt.ylim((-2,3))

    plt.xlabel('I am x')
    plt.ylabel('I am y')

    new_ticks = np.linspace(-1,2,5)    #  改变刻度
    print(new_tricks)
    plt.xticks(new_ticks)

    plt.yticks([-2, -1.8, -1, 1.22, 3],[r'$really\ bad$', r'$bad\ \alpha$', r'$normal$', r'$good$', r'$really\ good$'])   #改变为特殊的刻度


    plt.show()
```
结果如图


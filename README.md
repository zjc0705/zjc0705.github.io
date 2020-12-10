# zjc0705.github.io
---
title: 小三角如何制作
date: 2020-11-14 13:34:07
tags:
---
---
 
 
  
 


## 有时候我们需要制作一个小三角，比如要向下的三角，就要用到border-top，border-left，border-right。
## 废话不多说，看下面的代码

``` bash
 width:0;
 height:0;
 border-top:12px   solid #123
 border-left:12px  solid transparent
 border-right:12px solid transparent
 ```
 ## 解释一下，我们要让div宽高都是0，这样扩展的都是边框，上边让他有颜色，然后左边和右边都transparent，让他消失。
 ## 补充：transparent是全透明黑色(black)的速记法，即一个类似rgba(0,0,0,0)这样的值。在CSS1中，transparent被用来作为background-color的一个参数值，用于表示背景透明。
## 在CSS2中，border-color也开始接受transparent作为参数值，《Open eBook(tm) Publication


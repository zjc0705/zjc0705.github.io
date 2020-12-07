---
title: margin击穿和高度塌陷和边距负值和三栏布局
date: 2020-11-19 16:14:26
tags:
---
## marign击穿就是边距叠加，当两个兄弟盒子son和son1垂直相邻并且是块级元素的时候，会发生margin击穿。注意：水平方向并不会发生击穿，padding则会变成增加块的高宽，float也不会，并且行内元素不存在有margin这说法
## 当给son margin-bottm30px。并且给son1margintop50px
这个时候他们的距离不是60而是50px，取他们的大值。这个就是击穿
```bash

<body>
   ---边距叠加
   <!-- <div class="son"></div> 
   <div class="son1"></div>

<span class="s1">djflkdjfkjflkdj</span>
<br>

<span class="s2"> 123432432453543</span>
 -->
 <div class="father">
     <div class="son"></div>
     <div class="son1"></div>
    <!-- <div>dsjfjdkfjd</div> -->
 </div>

</body>
<style>
.father{
    width: 500px;
    height: 400px;
    background-color: darkgreen;
   /*  margin-top: 30px; */
   /*  margin-bottom: 40px; */
   /*  padding-top: 30px; */
 /*    padding-bottom: 40px; */
 /* border: 1px solid #123456; */
 overflow: auto;
}
.father::after{
    content: "gggg";
    /* display: table; */
    /* display: block; */
}

    .son{
        width: 200px;height: 200px;
        background-color: chocolate;
     /*  margin-right: 30px;  */
    /*  padding-right: 30px; */
   /*  margin-top: 30px; */
   /*  margin-bottom: 40px; */
    /* padding-top: 30px; */
  /*   padding-bottom: 40px; */
     }
    .son1{
        width: 50px;
        height: 50px;
        background-color: blue;
        /* margin-top: 30px; */
       /*  margin-bottom: 30px; */
    }
```
##  如果是父亲和儿子的关系的时候，明明只想改变儿子的margintop，但是父亲跟着一起动了。
## 解决方法1 给父亲一个border，让儿子知道一它为边界运动
## 2 给父亲添加一个overflow：auto，但是这个方法不可控，也是未知的，所以最好别用
## 3:给父亲一个伪类：
```bash

.father::after{
    content: "gggg";
   1 /* display: table; */ 这个会让其变成table，不会独占一行
   2 /* display: block; */这个会让其变成block，会独占一行
    
```

## 水平方向的定位，当给son1加定位，给son marginright，没有看见右边移动，因为son没有参考的，其实盒子模型是生效了的。但是页面看不见。
## 边距负值 菜单栏会用到

## 文档流元素按照，从左到右，从上到下的排列顺序，就是文档流
## 当元素float：left的时候，都是水平排列，并且，第一个挨着第二个这样。
## 一旦屏幕没有那么大，装不下的时候，最后一个会被挤下来，但是并不是换行，而是按照最小的能够放下的位置。
## 定位大于浮动，意思是定位的会覆盖住浮动的

## 高度塌陷 就是当父亲不设置高度宽度的时候,几个儿子都浮动left，本来应该撑起来父亲，但是并没有。

## 方法如下
## 1 给父亲也加float：left但是这样的话后面又要给爷爷，爷爷的父亲都要加浮动，太麻烦了

 
## 2给父亲加overflow：hidden 这样对下拉菜单不是友好

## 3让父亲display：inline-block 
## 4 position： relative和abusolute都行 但是这样会对页面的其他元素造成影响，因为他一旦浮动起来了就脱离了文档流
## 5 添加一个空白块，在几个儿子的后面让他clear：both
 
## 6 给父亲添加一个伪元素 .father::after{content: "";  clear: both;   height: 0; display: block;
 
   
  
   
```bash
.father{
    border: 1px solid #000;
    /*  float: left;  */  
  /*   overflow: hidden;   */
  /* position: relative; */ /* position: absolute; *//* top: 10px; */
 /*  display: inline-block;
   */
  /*  height: 100px;
   width: 1000px; */
  }
  
.son{
    width: 50px;
    height: 50px;
    background-color: maroon;
     float: left; 
    /*  display: inline-block;  */ 

}

.son1{
width: 100px;
height: 100px;
background-color: mediumblue;

float: left; 
 /*  display: inline-block;  
 */
}
 /* .s{
    clear: both;
}   */
/* .father::after{
    content: "";
    clear: both;
    height: 0;
    display: block;
}  */
```

## 三栏布局 解释在里面
```bash
  <div class="clear">
        <div class="father">

          // 注意这个cont一定要写在left和right的前面不然会出错
          因为当他写在下面的时候，首先会被left这个块挤下来，即使是浮动了的。 
            <div class="cont">

              <div class="main">
<h2 style="background-color: blue;">这个是内容哒哒哒哒哒哒单独</h2>
 
        </div>
        </div>
        <div class="left">左边菜单吧</div>
    
      
        <div class="right">右边菜单</div>
        
    </div>
    </div>
    <div>好地方极乐迪斯科父级</div>
</body>
<style>
      *{
        margin: 0;
        padding: 0;
    }  
     .father{
 border:1px solid #000;

 
    }  

    .left{
        width: 100px;
        height: 100px;
        background-color: red;
        float: left;
         margin-left: -100%;  
        
    }
    .right{
        width: 100px;
        height: 100px;
        background-color: mediumspringgreen;
        float: left;
        margin-left: -100px;  
    }
    .cont{
        
        width: 100%;
        background-color: orange;
        float: left;
    }
     .main{
  margin: 0 100px 0 100px;  
 
 
    } 
    .clear::after{
        content: "";
        display: block;
        clear: both;
    }   

```
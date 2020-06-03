### 1. 什么是CSS

如何学习：

1. CSS是什么
2. CSS怎么用（快速入门）
3. **CSS选择器（重点 + 难点）**
4. 美化网页（文字、阴影、超链接、列表、渐变...）
5. 盒子模型
6. 浮动
7. 定位
8. 网页动画（特效）

#### 1.1  什么是CSS

cascading style sheet  层叠级联样式表

CSS：表现层（美化网页）

字体，颜色，边距，高度宽度，背景图片，网页定位，网页浮动

![image-20200520090748147](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200520090748147.png)

#### 1.2 CSS发展史

CSS 1.0

CSS 2.0　　DIV（块）＋CSS,提出HTML与CSS分离的思想,网页变得简单,SEO

CSS 2.1  浮动,定位

CSS 3.0　圆角，阴影，动画...

注意浏览器兼容性



#### 1.3 CSS快速入门

 ![image-20200520092832444](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200520092832444.png)



**css的优势**:

1. 内容和表现分离
2. 网页结构表现同一,可以实现复用
3. 样式丰富
4. 建议使用独立于HTML的CSS文件
5. 利于SEO，容易被搜索引擎收录



#### 1.4 CSS的3种导入方式

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <!--内部样式-->
    <style>
        h1{
            color: aqua;
        }
    </style>

</head>
<body>
<!--优先级：就近原则，谁离得近，就用谁的样式  覆盖原则？？近的样式覆盖远的样式-->


<!--外部样式-->
<link rel="stylesheet" href="CSS/style.css">

<!--行内样式：在标签元素中，编写一个style属性，编写样式即可-->
<h1> 一级标题</h1>

</body>
</html>
```

3种导入样式优先级: 遵循就近原则



扩展:外部样式两种写法

- 链接式

    link属于html标签

    ```html
    <link rel="stylesheet" href="CSS/style.css">
    ```

- 导入式

    ​	@import是CSS2.1特有的

    ```html
    <!--导入式-->
    <style>
     @import url(CSS/style.css);
    </style>
    ```



### 2.选择器

**作用:**选择页面上某一个或某一类元素

#### 2.1 三种基本选择器

1. 标签选择器   选择一类标签     格式:   标签名{}

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>标签选择器</title>
        <style>
            /*标签选择器会选中页面上所有的这个标签元素*/
            h1{
                color: #ee481e;
            }
    
            p{
                font-size: 50px;
            }
        </style>
    
    </head>
    <body>
    
    <h1>标签选择器</h1>
    <h1>标签选择器</h1>
    
    <p>CSS 学习</p>
    </body>
    </html>
    ```

2. 类选择器    class:选中所有class属性一致的标签,跨标签     格式:  .类名{}

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>类选择器</title>
    
        <style>
            /*
            类选择器的格式： .class的名称{}
            优点：可以多个标签归类，是同一个class
            */
            .zh{
                color: blue;
            }
            .wss{
                color: brown;
            }
    
        </style>
    
    </head>
    <body>
    
    <h1 class="zh">1</h1>
    <h1 class="zh">2</h1>
    <h1 class="wss">3</h1>
    
    </body>
    </html>
    ```

3. id选择器     全局唯一    格式:   #id名{}

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>id选择器</title>
        <style>
            /*
                id选择器：id必须全局唯一
                格式：#id名称{}
                优先级 不遵循就近原则
                id选择器  >  class选择器  >  标签选择器
            */
            #zzz{
                color: darkblue;
            }
    
            .zh{
                color: aliceblue;
            }
        </style>
        
    </head>
    <body>
    
    <h1 id="zzz">1</h1>
    <h1 class="zh">2</h1>
    <h1>3</h1>
    <h1>4</h1>
    <h1>5</h1>
    
    </body>
    </html>
    ```

三类选择器的优先级 : 不遵循就近原则

> id选择器>类选择器>标签选择器



#### 2.2 层次选择器

1. 后代选择器:在某个元素的后面,例如爷爷==>爸爸==>儿子

    ```css
    /*后代选择器*/
    body p{
    	background: #ee481e;
    }
    ```

2. 子选择器:  某个元素后的一代  

    ```css
    /*子选择器*/
    body>p{
    	background: blue;
    }
    ```

3. 相邻兄弟选择器:  兄弟姐妹

    ```css
    /*相邻兄弟选择器  只有一个，向下相邻*/
    .active + p{
    	background: coral;
    }
    ```

4. 通用兄弟选择器

    ```css
    /*通用兄弟选择器，当前选中元素的向下所有兄弟元素*/
    .active~p{
    	background: darkgreen;
    }
    ```

    

  ![image-20200520105010237](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200520105010237.png)



#### 2.3 结构伪类选择器

```css
/*ul的第一个子元素*/
        ul li:first-child{
            background: darkgreen;
        }
        /*ul的最后一个子元素*/
        ul li:last-child{
            background: blue;
        }

        /*选中p1：定位到父元素，选择当前的第一个元素
        选择当前p元素的父元素，然后再选择父元素的第一个，并且这个元素是当前的元素才能生效
        */
        /*直接通过数量选择   数字代表第几个*/
        p:nth-child(1){
            background: #e9ee76;
        }

        /*根据类型选择*/
        p:nth-of-type(2){
            background: darkmagenta;
        }
```



#### 2.4 属性选择器

> =是绝对等于
>  *=是包含于
>  ^=是以此为开头
>  $=是以此为结尾

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>属性选择器</title>

    <style>
        .demo a{
            float: left;
            display: block;
            height: 50px;
            width: 50px;
            border-radius: 10px;
            background: salmon;
            text-align: center;
            text-decoration: none;
            margin-right: 5px;
            line-height: revert;
        }

        /*属性名，属性名 = 属性值（可以用正则表达式）
         =是绝对等于
         *=是包含于
         ^=是以此为开头
         $=是以此为结尾
        */
        /*存在id属性的元素   a[]{}*/
        /*a[id]{*/
        /*    background: brown;*/
        /*}*/

        a[id = first]{
            background: brown;
        }

        /*class 中有links的元素*/
        a[class *= links]{
            background: #000000;
        }

        /*选中href中以https开头的元素*/
        a[href ^= https]{
            background: fuchsia;
        }

        /*选中以pdf结尾的元素*/
        a[href $= pdf]{
            background: chocolate;
        }

    </style>

</head>
<body>

<p class="demo">
    <a href="https://www.baidu.com" class="links item first" id="first">1</a>
    <a href="" class="links item active" target="_blank" title="test">2</a>
    <a href="image/1.html" class="links item">3</a>
    <a href="image/1.jpg" class="links item">4</a>
    <a href="/1.pdf" class="links item">5</a>
    <a href="/1.docx" class="links item">6</a>
    <a href="" class="links item last">7</a>

</p>

</body>
</html>
```



### 3. 美化网页元素

#### 3.1 

span标签：重点要突出的字用span标签包裹起来（约定俗成）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>span标签</title>
    <style>
        #t1{
            font-size: 20px;
        }
    </style>

</head>
<body>
欢迎学习<span id = "t1">java</span>
</body>
</html>
```



#### 3.2 字体样式

```html
<!--
    font-family：字体样式(宋体、黑体等等)
    font-size:字体大小
    font-weight:字体粗细
	color:颜色
    -->

    <style>
        body{
            font-family: 楷体;
            color: darkmagenta;
        }

        h1{
            font-size: 50px;
        }
        .p1{
            font-weight: revert;
        }

    </style>
```



#### 3.3 文本样式

1. 颜色    color，几种书写方式：单词、RGB值、RGBA
2. 文本对齐方式     text-align
3. 首行缩进   text-indent
4. 行高  line-height   单行文字上下居中，line-height = height即可 
5. 装饰   text-decrotion

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>文本样式</title>

    <!--
        颜色：几种表示方式
        1.直接用单词
        2.RGB表示   0~F  十六进制
        3.REBA表示   A代表透明度 范围为0~1
        text-align:文字的排版
        text-indent:首行缩进，一般用em为单位，一个em代表一个字
        height: 200px;
        line-height: 200px;
        行高和块的高度一致就可以垂直居中
    -->
    <style>
        h1{
            color: rgba(40%,10%,70%,0.3);
            text-align: center;
        }
        .p1{
            text-indent: 2em;
        }
        .p2{
            height: 200px;
            line-height: 200px;  
        }

        /*下划线*/
        .l1{
            text-decoration: underline;
        }
        /*中划线*/
        .l2{
            text-decoration: line-through;
        }
        /*上划线*/
        .l3{
            text-decoration: overline;
        }
        /*超链接去下划线*/
        a{
            text-decoration: none;
        }

        /*图像与文本对齐*/
        img，span{
            vertical-align: middle;
        }
    </style>


</head>
<body>

<a href="">111111</a>
<p class="l1">1111</p>
<p class="l2">1111</p>
<p class="l3">1111</p>

<h1>航海王</h1>

<p class="p1">《航海王》是日本漫画家尾田荣一郎作画的少年漫画作品，在《周刊少年Jump》1997年12月24日开始连载。</p>

<p>改编的电视动画《航海王》于1999年10月20日起在富士电视台首播。<p/>

<p class="p2">2012年5月11日，《航海王》获得第41回日本漫画家协会赏。</p>

<p>截至2015年6月15日，《航海王》以日本本土累计发行了3亿2086万6000本，被吉尼斯世界纪录官方认证为“世界上发行量最高的单一作者创作的系列漫画” </p>

<p>2017年7月21日，日本纪念日协会通过认证，将每年的7月22日设立为“ONE PIECE纪念日”</p>

<p>
    <img src="image/1.jpg" alt="" height="500px" width="500px">
    <span>我要和图像对齐</span>
</p>
</body>
</html>
```



#### 3.4 阴影

```html
/*阴影效果 text-shadow：阴影颜色，水平偏移，垂直偏移，阴影半径*/
        #price{
            text-shadow: olivedrab 10px 10px 2px;
        }
```

#### 3.5 超链接伪类

重点是  a:hover{}

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>超链接伪类</title>

    <style>
        /*默认的颜色*/
        a{
            text-decoration: none;
            color: #000000;
        }
        /*鼠标悬浮的颜色  重点记忆*/
        a:hover{
            color: #ee481e;
        }

        /*鼠标按住未释放的效果*/
        a:active{
            color: blue;
        }

        /*已访问链接的颜色*/
        a:visited{
            color: blueviolet;
        }

        /*阴影效果 text-shadow：阴影颜色，水平偏移，垂直偏移，阴影半径*/
        #price{
            text-shadow: olivedrab 10px 10px 2px;
        }
    </style>

</head>
<body>

<a href="#">
    <img src="images/1.jpg" alt="">
</a>
<p>
    <a href="https://search.jd.com/" target="_blank">Java从入门到项目实战（全程视频版） 编程入门/IT计算机书籍</a>
</p>

<p>
    <a href="#">中国水利水电出版社</a>
</p>

<p id="price">
    ￥49.9
</p>
</body>
</html>
```



#### 3.6 列表

```css
#nav{
    width: 300px;
    height:300px;
}

.title{
    font-size: 20px;
    font-weight: bold;
    text-indent: 1em;
    line-height: 30px;
    background: #ee481e;
}

/*ul li*/
/*
list-style:
    none:去掉原点
    circle：空心圆
    decimal：数字
    square:正方形
*/
ul{
    background: burlywood;
}

ul li{
    height: 30px;
    list-style: none;
    text-indent: 1em;
}

a{
    text-decoration: none;
    font-size: 16px;
    color:#000000;
}

a:hover{
    color: bisque;
}
```

#### 3.7 背景

背景颜色

背景图片

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>背景</title>
    <style>
        div{
            width: 1000px;
            height: 800px;
            /*边框：粗细  样式  颜色*/
            border-radius: 2px;
            border-style: solid;
            border-color: red;
            background-image: url("images/d.png");
        }
        /*背景图片填充方式，默认填充满*/
        .div1{
            /*沿x方向填充*/
            background-repeat: repeat-x;
        }
        .div2{
            /*沿y方向填充*/
            background-repeat: repeat-y;
        }
        .div3{
            /*不填充，只有原来的图片*/
            background-repeat: no-repeat;
        }
    </style>

</head>
<body>

<div class="div1"></div>
<div class="div2"></div>
<div class="div3"></div>

</body>
</html>
```

#### 3.8 渐变

https://www.grabient.com/

复制可直接用

### 4.盒子模型

#### 4.1 基本概念

![image-20200525161642046](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200525161642046.png)

上图为一个盒子

margin：外边距

padding：内边距

border：边框

#### 4.2 边框

```css
/*边框： 大小  样式（虚线、实线）  颜色*/
div:nth-of-type(1)>input{
border: 1px solid #1d1709;
}
div:nth-of-type(2)>input{
border: 2px dashed #1d1709;
}
div:nth-of-type(3)>input{
border: 2px solid #1d1709;
}
```

#### 4.3 内外边距

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>外边距</title>
    <style>
        /*外边距的用处：居中*/
        h1,ul,li,a,body{
            margin: 0;
            padding: 0;
            text-decoration: none;
        }
        #box{
            width: 300px;
            border: 1px solid red;
            margin:0 auto;
        }
        form{
            background: rgba(164, 92, 75, 0.56);
            margin: 0 auto;
        }
        /*
        顺时针
        margin:0;   上下左右都为0
        margin：0 1px;   左右
        margin:上 右 下 左
        */
        h2{
            font-size: 30px;
            background-color: #6284FF;
            line-height: 30px;
            text-align: center;
            margin:1px 0;
        }
        div:nth-of-type(1)>input{
            border: 1px solid #1d1709;
            padding:1px;
        }
        div:nth-of-type(2)>input{
            border: 1px solid #1d1709;
            padding:0 2px;
        }
    </style>
</head>
<body>

<div id="box">
    <h2>会员登录</h2>
    <form action="#">
        <div>
            <span>用户名：</span>
            <input type="text">
        </div>

        <div>
            <span>邮箱：</span>
            <input type="text">
        </div>

        <div>
            <span>密码：</span>
            <input type="password">
        </div>
    </form>
    
</div>
</body>
</html>
```

盒子的计算方式：这个元素到底多大？？

![image-20200528163854016](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200528163854016.png)

margin + border + padding + + 内容宽度



#### 4.4 圆角边框

border-radius

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>圆角边框</title>

    <!--左上  右上  右下 左下  顺时针-->
    <!--画圆    圆角 = 半径？-->
    <style>
        div{
            width: 100px;
            height: 100px;
            border: 10px solid red;
            border-radius: 100px;
        }
    </style>

</head>
<body>

<div>

</div>
</body>
</html>
```

#### 4.5 阴影

shadow

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>阴影</title>
    <style>
        div{
            width: 100px;
            height: 50px;
            border: 2px solid red;
            box-shadow: 10px 10px 100px yellow;
        }
    </style>
    
</head>
<body>
<div></div>
</body>
</html>
```

### 5. 浮动

#### 5.1 标准文档流

![image-20200528180034135](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200528180034135.png)

块级元素：独占一行

> h1~h8  p  div  列表...

行内元素：不独占一行

> span   a   img   strong...

行内元素可以包裹在块级元素中，但块级元素不能包裹在行内元素

#### 5.2 display

display：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>display</title>
    <!--
    block  块元素
    inline  行内元素
    inline-block   是块元素，但是可以内联在一行
    -->

    <style>
        div{
            width: 100px;
            height: 100px;
            border:1px solid red;
            display: inline-block;
        }

        span{
            width: 100px;
            height: 100px;
            border:1px solid red;
            display: inline;
        }

    </style>

</head>
<body>
<div>div块元素</div>
<span>span行内元素</span>
</body>
</html>
```

#### 5.3 float(浮动)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>浮动</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
<div id="father">
    <div class="layer1"><img src="images/0.jpg" alt=""></div>
    <div class="layer2"><img src="images/1.jpg" alt=""></div>
    <div class="layer3"><img src="images/5.jpg" alt=""></div>
    <div class="layer4">
        浮动的盒子可以向左浮动，也可以向右浮动，直到他的外边缘碰到包含框或另一个浮动盒子为止。
    </div>
</div>
</body>
</html>
```

```css
div{
    margin: 10px;
    padding: 5px;
}

#father{
    border: 1px solid #000;
}

.layer1{
    border: 1px dashed #F00;
    display: inline-block;
    float: right;
}

.layer2{
    border: 1px dashed #00F;
    display: inline-block;
    float: right;
}

.layer3{
    border: 1px dashed #060;
    display: inline-block;
    float: right;
}

.layer4{
    border: 1px dashed #666;
    font-size: 14px;
    line-height: 23px;
    display: inline-block;
    float: right;
}
```



#### 5.4 父级边框塌陷问题

```css
clear:right  右侧不允许有浮动
clear:left   左侧
clear:both   两侧不允许有浮动
```

清除浮动解决方案：

1. 增强父级元素的高度

    ```css
    #father{
        border: 1px solid #000;
        height: 1000px;
    }
    ```

2. 增加一个空的div标签，清除浮动

    ```html
    <div class="clear"></div>
    
    .clear{
        clear: both;
    	margin:0;
    	padding:0;
    }
    ```

3. overflow

    ```css
    在父级元素中增加overflow:hidden
    ```

4. 在父类添加一个伪类：after

    ```css
    #father:after{
        content: '';
        display: block;
        clear: both;
    }
    ```

**清除浮动小结：**

1. 浮动元素后增加空div

    简单，但代码冗余

2. 设置父元素的高度

    新添加元素可能会撑开，同样会塌陷

3. overflow

    下拉的场景避免使用

4. 在父类添加一个伪类：after

    **推荐使用**，写法稍微复杂，但无副作用



#### 5.5 对比

- display

    方向不可以控制

- float

    浮动起来会脱离标准文档流，要解决父级边框塌陷的问题

### 6. 定位

#### 6.1 相对定位

position:relative;    相对定位

上下左右: top   bottom  left   right

相对于原来的位置，进行指定的偏移。相对定位，仍然在标准文档流中，原来的位置会保留。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>定位-默认情况</title>

    <style>
        div{
            margin: 10px;
            padding: 5px;
            font-size: 12px;
            line-height: 25px;
        }

        #father{
            border: 1px solid #0000FF;
        }
        /*
        position:relative;    相对定位
        上下左右: top   bottom  left   right
        意为距离其多少像素
        */
        #first{
            border: 3px dashed rgba(168, 100, 62, 0.64);
            position: relative;
            top: 10px;
        }

        #second{
            border: 3px dashed rgba(69, 210, 175, 0.89);
            position: relative;
            right: 10px;
        }

        #third{
            border: 3px dashed rgba(242, 42, 40, 0.42);
            position: relative;
            left: 20px;
            bottom: 10px;
        }
    </style>

</head>
<body>
<div id="father">
    <div id="first">第一个盒子</div>
    <div id="second">第二个盒子</div>
    <dv id="third">第三个盒子</div>
</div>
</body>
</html>
```

练习题：

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>练习</title>

    <link rel="stylesheet" href="css/style.css">

</head>
<body>

<div id="box">
    <div class="a1"><a href="#">链接1</a></div>
    <div class="a2"><a href="#">链接2</a></div>
    <div class="a3"><a href="#">链接3</a></div>
    <div class="a4"><a href="#">链接4</a></div>
    <div class="a5"><a href="#">链接5</a></div>
</div>

</body>
</html>
```

```css
a{
    text-decoration: none;
    color: white;
    display: block;
    width: 50px;
    height: 50px;
    text-align: center;
    line-height: 50px;
    background-color: #ff83db;
}
#box{
    margin: 0 auto;
    padding: 5px;
    width: 200px;
    height: 200px;
    border: 2px solid red;
}

a:hover{
    background-color: #3510ff;
}

.a2{
    position: relative;
    left: 150px;
    top:-50px;
}

.a3{
    position: relative;
    left: 75px;
    bottom: 25px;
}

.a5{
    position: relative;
    left: 150px;
    bottom:50px;
}
```

#### 6.2 绝对定位

**position: absolute;**

定位：基于xxx进行定位，上下左右

1. 没有父元素定位的情况下，相对于浏览器进行定位
2. 若父级元素存在定位，我们通常会相对于父元素进行偏移
3. 在父级元素范围内移动
4. 相对于父级或浏览器的位置，进行指定的偏移，绝对定位后，它不在标准文档流中，原位置不会被保留。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>定位-绝对定位</title>

    <style>
        div{
            margin: 10px;
            padding: 5px;
            font-size: 12px;
            line-height: 25px;
        }

        #father{
            border: 1px solid #0000FF;
            position: relative;
        }

        /*
        position:relative;    相对定位
        上下左右: top   bottom  left   right
        意为距离其多少像素
        */
        #first{
            border: 3px dashed rgba(168, 100, 62, 0.64);
        }

        #second{
            border: 3px dashed rgba(69, 210, 175, 0.89);
            position: absolute;
            right: 20px;
        }

        #third{
            border: 3px dashed rgba(242, 42, 40, 0.42);
        }
    </style>

</head>
<body>
<div id="father">
    <div id="first">第一个盒子</div>
    <div id="second">第二个盒子</div>
    <div id="third">第三个盒子</div>
</div>
</body>
</html>
```



#### 6.3 固定定位

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>固定定位</title>
    <style>
        body{
            height: 1000px;
        }
        div:nth-of-type(1){
            width: 100px;
            height: 100px;
            background: red;
            position: absolute;
            right: 0;
            bottom: 0;
        }

        /*固定定位 position: fixed;*/
        div:nth-of-type(2){
            width: 50px;
            height: 50px;
            background: black;
            position: fixed;
            right: 0;
            bottom: 0;
        }
    </style>

</head>
<body>

<div>div1</div>
<div>div2</div>
</body>
</html>
```

#### 6.4 z-index

一个层级的概念，例如图层一样

z-index：默认值为0，最高无限制

背景透明度：opacity

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>z-index</title>

    <link rel="stylesheet" href="css/style.css">

</head>
<body>

<div id="content">
    <ul>
        <li><img src="images/5.jpg" alt=""></li>
        <li class="tipText">z-index学习</li>
        <li class="tipBackground"></li>
        <li>时间：2020/5/31</li>
        <li>地点：deyang</li>
    </ul>
</div>
</body>
</html>
```

```css
#content{
    height: 960px;
    width: 1400px;
    border: 1px solid black;
    padding: 0px;
    margin: 0px;
}

ul li{
    padding: 0px;
    margin: 0px;
    list-style: none;
}
/*父级元素相对定位*/
#content ul{
    position: relative;
}

.tipText,.tipBackground{
    width: 1200px;
    height: 25px;
    position: absolute;
    top: 810px;

}
.tipBackground{
    background: #000000;
    opacity: 0.5;
}
.tipText{
    /*z-index: 9;*/
    color: white;
}
```

### 7. 动画
### 基本概念

-  W3C标准
    
    - 结构化标准语言(HTML、XML)
    - 表现标准语言(CSS)
    - 行为标准(DOM、ECMAScript)
    
- 块元素
    - 无论内容多少，该元素独占一行
    - p标签、h1--h6标签等等
    
- 行内元素
    - 内容撑开宽度，左右都是行内元素的可以排在一行
    - a标签、strong标签等等

- 列表

- 表格

- 视频和音频

- 页面结构分析

    ![image-20200519223914563](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200519223914563.png)

- iframe内联框架

:star:**表单**

![image-20200519230501505](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200519230501505.png)

![image-20200519230526163](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200519230526163.png)  

**总结**

![image-20200520003113719](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200520003113719.png)



### 代码

#### 1.helloworld

```html
<!-- DOCTYPE:告诉浏览器使用的规范 -->
<!DOCTYPE html>
<html lang="en">
<!--head标签代表网页头部-->
<head>
    <!--meta描述性标签，它用来描述网页的一些信息-->
    <!--meta标签一般用来做SEO-->
    <meta name = "keywords" content = "html学习">
    <meta name = "description" content="Java学习">
    <meta charset="UTF-8">
    <!--  title网页的标题 -->
    <title>HiWorld</title>
</head>
<body>
Hello World!!
</body>
</html>
```

#### 2.基本标签

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>基本标签学习</title>
</head>
<body>

<!--标题标签-->
<h1>一级标签</h1>
<h2>二级标签</h2>
<h3>三级标签</h3>
<h4>四级标签</h4>
<h5>五级标签</h5>

<!--段落标签-->
<p>跑得快 跑得快</p>
<p> 11111111</p>
<p> 22222222222 </p>

<!--换行标签-->
跑得快<br/> 跑得快<br/>

<!--水平线标签-->
<hr>

<!--粗体、斜体-->
<h1>字体样式标签</h1>
<strong>Strong是粗体标签</strong>
<b>b也是粗体标签？？</b>
<br>
<em>em是斜体标签</em>

<hr>
<!--特殊符号-->
&nbsp;空格 &nbsp;

<br/>
&gt;   大于符号
<br/>
&lt;   小于符号

<br/>

&copy;  版权符号
</body>
</html>
```

#### 3.图像标签

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>图像标签学习</title>
</head>
<body>

<!--img标签学习
src：图片地址
    相对地址、绝对地址
    ../  代表上一级目录
alt：图片名字

title：悬停文字：鼠标放上去时显示的文字
    -->
<img src="../resources/image/5.jpg" alt="图像5" title="这是悬停文字！" width="500" height="500">

<a href="4.链接标签.html#down"> 跳转</a>
</body>
</html>
```

#### 4.链接标签

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>链接标签学习</title>
</head>
<body>

<!--使用name作为标记  与锚链接结合使用-->
<a name="top">顶部</a>

<!--
a标签学习：
    href：表示跳转到哪个页面
    target：表示窗口在哪里打开
        _blank:在新标签页打开
        _self:在自己的网页中打开
-->
<a href="3.图像标签.html" target="_blank"> 点击打开新网页 </a>
<br/>
<a href="https://www.baidu.com" target="_self"> 点击跳转 </a>

<br/>
<!--用图像来跳转网页-->
<a href="1.HelloWorld.html">
    <img src="../resources/image/5.jpg" alt="图像5" title="这是悬停文字！" width="500" height="500">
</a>
<a href="1.HelloWorld.html">
    <img src="../resources/image/5.jpg" alt="图像5" title="这是悬停文字！" width="500" height="500">
</a>
<a href="1.HelloWorld.html">
    <img src="../resources/image/5.jpg" alt="图像5" title="这是悬停文字！" width="500" height="500">
</a>
<a href="1.HelloWorld.html">
    <img src="../resources/image/5.jpg" alt="图像5" title="这是悬停文字！" width="500" height="500">
</a>
<!--
锚链接：
1.需要一个锚标记
2.跳转到标记  用#
-->

<a href="#top">回到顶部</a>
<a name="down">down</a>


<!--
功能性链接
邮件链接：mailto
-->

<a href="mailto:12345@qq.com">点击联系我</a>
</body>
</html>
```

#### 5.列表

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>列表学习</title>
</head>
<body>

<!--
有序列表:
    应用于试卷、问卷等等
-->
<ol>
    <li>java</li>
    <li>C</li>
    <li>linux</li>
    <li>python</li>
</ol>

<hr>
<!--
无序列表:
    应用于导航、侧边栏
 -->
<ul>
    <li>java</li>
    <li>C</li>
    <li>linux</li>
    <li>python</li>
</ul>

<hr>
<!--
自定义列表
    dl：标签
    dt：列表名称
    dd：列表内容
应用于公司网站底部
-->
<dl>
    <dt>学科</dt>
    <dd>java</dd>
    <dd>python</dd>
    <dd>css</dd>
    <dd>mysql</dd>

    <dt>老师</dt>
    <dd>java</dd>
    <dd>python</dd>
    <dd>css</dd>
    <dd>mysql</dd>
</dl>

</body>
</html>
```

#### 6.表格

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>表格学习</title>
</head>
<body>

<!--
表格 table
行  tr
列  td
-->
<table border="1px">
    <tr>
        <!--colspan 跨列-->
        <td colspan="4">1-1</td>
    </tr>
    <tr>
        <!--rawspan 跨行-->
        <td rowspan="2">2-1</td>
        <td>2-2<td>
        <td>2-3</td>
        <td>2-4</td>
    </tr>
    <tr>
        <td>3-1</td>
        <td>3-2<td>
        <td>3-3</td>
    </tr>
</table>

<hr>
<table border="1px">
    <tr>
        <td colspan="3">学生成绩</td>
    </tr>

    <tr>
        <td rowspan="2">zh</td>
        <td>语文</td>
        <td>100</td>
    </tr>

    <tr>
        <td>数学</td>
        <td>100</td>
    </tr>

    <tr>
        <td rowspan="2">wss</td>
        <td>语文</td>
        <td>100</td>
    </tr>

    <tr>
        <td>数学</td>
        <td>100</td>
    </tr>
</table>

</body>
</html>
```

#### 7.媒体元素

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>媒体元素学习</title>
</head>
<body>

<!--音频和视频
src:资源路径
controls:控制条
autoplay：控制自动播放
-->

<video src="../resources/video/Foryou.mp4" controls autoplay></video>
<audio src=""></audio>
</body>
</html>
```

#### 8.页面结构

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>页面结构分析</title>
</head>
<body>

<header>
    <h2>网页头部</h2>
</header>

<section>
    <h2>网页主题</h2>
</section>

<footer>
    <h2>网页脚部</h2>
</footer>
</body>
</html>
```



#### 9.内联框架iframe

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>内联框架iframe</title>
</head>
<body>

<!--<iframe src="//player.bilibili.com/player.html?aid=55631961&bvid=BV1x4411V75C&cid=97257967&page=11"-->
<!--        scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>-->

<!--
iframe内联框架
src : 地址
width,height: 宽度，高度
-->
<iframe src="https://www.baidu.com" frameborder="0" width="800px" height="800px">
</iframe>

<iframe src="" name="框架标识名"></iframe>
<a href="https://www.baidu.com" target="框架标识名">点击跳转</a>
</body>
</html>
```



#### 10.表单（重点）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>表单学习</title>
</head>
<body>

<h1>注册</h1>

<!--
表单： form
action：表单提交的位置，可以是网站，也可以是一个请求处理地址
method：post，get提交方式
    get方式提交：可以在url中看到提交的信息，不安全  但是高效
    post：比较安全，传输大文件
readonly  只读
disabled   禁用
hidden   隐藏
-->
<form action="1.HelloWorld.html" method="get">
    <!--
    文本输入框：input type = "text"
    value="zhzh"   默认初始值
    maxlength="10"  最长能写几个字符
    size="30"      文本框长度
    placeholder="请输入用户名"     提示信息，用于输入框中
    required   非空判断
    -->
    <p>名字：<input type="text" name="username" placeholder="请输入用户名" required></p>

    <!--密码框：input type = "password"-->
    <p>密码：<input type="password" name="pwd"></p>

    <!--
    单选框标签  radio
    value 单选框的值
    name  表示给单选框分组，name的值必须相同，否则就不在一个组中，跟多选框没有区别
    -->
    <p>
        性别：
        <input type="radio" value="boy" name="gender" checked/>男
        <input type="radio" value="girl" name="gender"/>女
    </p>

    <!--
    多选框 checkbox
    checked 默认选中
    -->
    <p>
        爱好：
        <input type="checkbox" value="看书" name="hobby" checked>看书
        <input type="checkbox" value="打球" name="hobby">打球
        <input type="checkbox" value="看电视" name="hobby">看电视
        <input type="checkbox" value="看电影" name="hobby">看电影
    </p>

    <!--
    按钮  button
    input type="button"   普通按钮
    input type="image"    图像按钮
    input type="submit"   提交按钮
    input type="reset"    重置按钮
    -->
    <p>
        按钮：
        <input type="button" name="btn" value="点击按钮">
<!--        <input type="image" src="../resources/image/5.jpg">-->
    </p>

    <!--下拉框，列表框-->
    <p>
        地区：
        <select name="列表名称" >
            <option value="cn">CN</option>
            <option value="us">US</option>
            <option value="as">AS</option>
            <option value="hk">HK</option>
        </select>
    </p>

    <!--
    文本域  textarea
    -->
    <p>
        反馈：
        <textarea name="textarea" cols="50" rows="10">文本内容</textarea>
    </p>

    <!--文件域 input type="file" name="files"-->
    <p>
        <input type="file" name="files">
        <input type="button" value="上传" name="upload">
    </p>

    <!--邮件验证-->
    <p>
        邮箱：
        <input type="email" name="email">
    </p>

    <!--URL-->
    <p>
        URL：
        <input type="url" name="url">
    </p>

    <!--数字-->
    <p>
        数字：
        <input type="number" name="num" value="1" max="1000" min="0" step="1 ">
    </p>

    <!--滑块 -->
    <p>
        音量：
        <input type="range" name="voice" min="0" max="100">
    </p>

    <!--搜索框 -->
    <p>
        搜索：
        <input type="search" name="search">
    </p>

    <!--
    自定义邮箱
    pattern  正则表达式判断
    -->
    <p>
        自定义邮箱:
        <input type="email" name="diyemail" pattern="^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$">
    </p>

    <p>
        <input type="submit">
        <input type="reset">
    </p>
</form>

</body>
</html>
```


## 1.HTML

```html
<!DOCTYPE html>
<html lang='en'>    
<head>
    <meta charset='UTF-8'></meta>
    <link rel='stylesheet' href='https:///www.google.com/static/css'></link>
	<script src=''></script>
    <title>Document</title>
</head>
<body>
    <div>这是一个HTML文档!</div>
</body>
</html>
-----------------------------------------------------------------------------
HTML，超文本标记语言（英语：HyperText Markup Language，简称：HTML）是一种用于创建网页的标准标记语言。
```

### 标签&&属性

#### 单标签

> 只有开始标签，无结束标签

```html
<img src=''>   
<input type='text' name='username'>
```

#### 双标签

```html
<h1></h1>~~~<h6></h6>     # 标题标签
<div></div>   <a></a>   <p></p>   <span></span>   
<form action='' method=''></form>   
<b></b>   <i></i>   <em></em>   <strong></strong>
```

#### 语义化标签

```html
<header>头部</header>
<main>主体</main>
<nav>导航栏</nav>
<aside>侧导航栏</aside>
<footer>底部</footer>
```

#### 表单控件

> <form name='' action='' method=''>我是一个表单</form>

- name		-- 用来标识这个表单,可以通过document.表单名来获取这个表单
- action             -- 表示这个表单提交时的处理路径
- method          --  表单的提交方式，post和get方式，默认为get方式
  - get，通过地址栏传输数据，将数据通过？和url连接起来，多个参数之间用&连接 且对数据长度有限制，多数浏览器为2k，服务器为64k.
  - post, 通过request body 传输数据

##### get方式和post方式有什么不同

``` html
同：本质并无差别，使用的都是http协议建立的TCP连接来传输数据
异：GET产生一个TCP数据包，POST产生两个TCP数据包
```

一个完整的form表单

```html
<form name='regist' action='/app.py' method='get/post'>
    <span>用户名:</span><input type='text' palceholder='请填入用户名:' name='userName' value='' maxlength='12'>
    <span>密 码:</span><input type='password' palceholder='请填入密码:' name='userPassword' value='' maxlength='16'>
    <span>性 别:</span>
    <label for='man'>
        男:<input type='radio' name='sex' id='man'>
    </label>
    <label for='woman'>
        女:<input type='radio' name='sex' id='woman'>
    </label>
    <select name="XueWei" id="">
		<option value="">学士</option>
		<option value="">硕士</option>
		<option value="">博士</option>
	</select>
    <span>请选择你喜欢的音乐</span>
    	流行：<input type="checkbox">
    	古典：<input type="checkbox">
    	嘻哈：<input type="checkbox">
    请上传文件：<input type="file">
    <textarea type="" id="" row="" cols="">         //resize: none/both(水平和垂直		方向拖动)/valertical(垂直方向拖动)/horizont(水平方向拖动)
    </textarea>
	<input type="submit" name='提交'>
	<input type="resit" name='重置'>
    年、月:<input type="month">
    年、周:<input type="week">
    时、分:<input type="time">
    年、月、日:<input type="date">
    年、月、日、时、分:<input type="datetime-local">
    <input type="email">
    <input type="tel" autofocus>
</form>
```

#### 音频/视频标签

- <audio src="" controls loop></audio>
  - controls:控件想用户显示
  - loop:循环播放
  - autoplay:页面加载完后自动播放
- <video src="" controls loop autoplay></video>

#### 快速创建标签

```html
1.   div*n             #  创建n个div
2.   (div.className)*n       #  创建n个类名为className的DIV
3.   (div{内容}*n)         #  创建n个内容指定的DIV
4.   (div.className${内容}*n)       # 创建n个不同类名的DIV
```

## 2.CSS

> CSS 指层叠样式表 (**C**ascading **S**tyle **S**heets)

### 选择器

- 通用选择器   *{}

```css
*{
    margin: 0;             # 样式名：样式值
    padding: 0;
    list-style: none;
}
```

- 标签选择器  div{}

```css
div{
    width: 100%;            # 样式名：样式值
    height: auto;
    background: #f5f5f5;
}
```

- 类名选择器  .banner{}

```css
.banner{
    width: 100%;            # 样式名：样式值
    height: auto;
    background: #ff6700;
}
```

- 后代选择器  E1 E1{}

```css
.bigbox .smallbox{
    width: 100%;
    height: auto;
}
```

- ID选择器

```css
#idName{
    width: 100%;
    height: auto;
}
```

- 伪元素选择器

```css
::before{              #  在元素内容之前插入一个元素
    content:'';
}
::after{               #  在元素内容之后插入一个元素
    content:'';
}
```

- 伪类选择器

```css
element:hover{          #  鼠标移入该元素之后触发动作
    color: red;
}
```

- 伪结构选择器

```css
E:first-child{
    #    作为第一个孩子的E标签；匹配的是某父元素的第一个子元素，可以说是结构上的第一个子元素
}
E:first-of-type{
    #   作为子元素同类型的第一个；匹配的是该类型的第一个，类型是指什么呢，就是冒号前面匹配到的东西，比如 p:first-of-type，就是指所有p元素中的第一个。这里不再限制是第一个子元素了，只要是该类型元素的第一个就行了，当然这些元素的范围都是属于同一级的，也就是同辈的。
}
E:last-child{
    #    作为最后一个孩子的E标签
}
E:last-of-type{
    #   作为子元素同类型的最后一个
}
E:nth-child(n){
    #   选中作为孩子的第N个E标签
}
E:nth-of-type(arg){
    #   选中作为子元素的同类型的第N个
}
E:nth-last-child(arg){
    #   选中作为子元素的同类型的倒数第arg元素
}
#  arg可取  num(数字)/even(偶数)/odd(奇数)/表达式(3n--->3的倍数)
```

- 相邻兄弟选择器

```css
E1+E2{
    #   选择E1的下一个兄弟元素E2
}
```

- 群组选择器

```css
E1,E2,E3{         #  选择页面中所有的E1，E2，E3元素
    样式名：样式值;
}
```

- 属性选择器

```css
[attr]{}	#选择所有拥有attr属性的元素
E[attr="value"]		#选择拥有attr属性，并且属性值为value的元素
E[attr~="value"]	#选择拥有attr属性，并且属性值为一个或多个其中一个属性值为value的元素
E[attr^="value"]	#选择拥有attr属性，并且属性值为一个或多个其中一个属性值以为value开头的元素
E[attr$="value"]	#选择拥有attr属性，并且属性值一个或多个其中一个属性值以value结尾的元素
E[attr*="value"]	#选择拥有attr属性，并且属性值一个或多个其中一个属性值包含value的元素
```

### 选择器的优先级

> css3中使用5位数a,b,c,d,e判断优先级

```css
a----->行内样式   则a+=1
b----->ID选择器
c----->类名选择器
d----->标签选择器
e----->通用选择器
#   判断优先级的宗旨：越具体的优先级越高
#   id  100；className  10;标签名   1
```

### CSS样式表引入方式

- 外链式

```css
<link href='' rel='stylesheet'></link>
```

- 嵌入式

```css
<style></style>
```

- 行内样式

```css
<div style='color: red;background: blue;'></div>
```

### CSS中颜色的表示方式

- 预定义颜色

```css
color: red/blue/yellow/pink/blank......;
```

- 用十六进制数表示的颜色

```css
color: #ff6700/#f5f5f5;
```

- RGB颜色

```css
color: rgb([0-255],[0-255],[0-255]);
```

- RGBA带透明度的RGB

```css
color: rgba([0--255],[0--255],[0--255],[0-1]);
```

### CSS常用属性值的设置

#### 阴影的设置

```css
box-shadow:	1px 2px 0px 1px rgba(0,0,0,.5);		# x轴的偏移量  y轴的偏移量  阴影的模糊程度  阴影的大小  阴影的颜色
```

#### 背景图的设置

```css
background-img:url();		#引入多张图片时用逗号隔开
background-size:100px auto;   		#背景的尺寸大小设置
background-repeat:no-repeat;		#背景图的重复效果
background-position:x y ;    			#属性的值可以为数值，方位值
```

#### 背景图位置的设置

```css
background-origin: padding-box;		#从padding内填充位置开始渲染（默认情况）
                   border-box			#从边框位置开始渲染
                   content-box		#从内容位置开始渲染
background-clip: padding-box;		#从padding内填充位置开始渲染（默认情况）
                 border-box;		#从边框位置开始渲染
                 content-box;		#从内容位置开始渲染
background-attachment: fixed;		#使得背景图渲染到浏览器当中
```

#### 其它

```css
box-sizing:border-box;      # 将边框大小算进内容里面
opacity: .5;                # 元素透明度的设置
backgroud: linear-gradient(top,颜色1,颜色2)      # 背景颜色线性渐变
第一个参数：渐变开始的方向：top left bottom right 25deg
颜色：red #fff  rgb(0,0,0) rgba(0,0,0,0.7)

```

### 2D&&3D属性

#### 2D平移

- transform: translate(x,y);            #     平移
- transform: rotate(180deg);         #     旋转
- transform: scale(0.8)                    #     缩放
- transform: skew()                          #     斜切

#### 2D过渡

```css
transition: all .5s;
transition-property: ;
transition-duration: ;                  #  过渡效果持续时间
transition-timing-function: easy;		#  贝塞尔曲线  
transition-delay: ;					   #  过度延迟时间
```

#### 3D效果

```css
transform-origin:;		#设置旋转源点
perspective: 800px;		#设置透视点
transform-style:preserve-3d;	#让父类中的子类也有3D效果
transform:  rotate3d(0,1,0, 1turn)		#设置3D旋转
```

### CSS中定义并使用动画

#### 定义动画

```css
@keyframes animationName{
    from{
        background: red;
    }
    to{
        background: blue;
    }
}
```

#### 挂在动画

```css
div{
    animation: animationName .3 infinite;
}

# animation-iteration-count: 3;		#设定动画的次数  属性：infinite(无限循环)
# animation-direction: alternate/normal;		#指定下一次动画是否为逆向
# animation-fill-mode: backwards/forwards;		#设置动画的结束状态
返回一开始状态/返回一当前状态
# animation-play-state: running;		#设置开始开始时间
```

### CSS中的页面布局

> 布局：按标签在页面中的呈现效果分类

#### 三种元素

##### 行内元素

> 在一行内显示,不可设置宽高

```css
<span>  <del>  <i>  <em>  <b>  <strong>  <a>  ...
```

##### 块元素

> 可以设置宽高,独占一行

```css
<div>   标题标签<h1--h6>   段落标签<p>,<pre>   列表标签<table>  <ul(无序列表)>  <ol(有序列表)>
```

##### 块元素

> 可以设置宽高，在一行内显示

```css
<img src=''>   <form action='' method='get/post'></form>
```

#### 元素的操作

##### 元素之间的转换

> 优先级高低：块元素 > 行内块元素 > 行内元素

- 转换为块元素

```css
display: block;
```

- 转换为行内元素

```css
display: inline;
```

- 转换为行内块元素

```css
display: inline-block;
```

##### 元素之间嵌套的规则

- 同一级别可以相互嵌套
- 级别高的元素可以嵌套级别低的元素
- 段落标签<p>只能嵌套行内元素
- a标签不可以嵌套a标签

#### 盒子模型

##### 盒子模型的组成

- margin

> 外边距：盒子与盒子之间的距离

- border

> 边框

- padding

> 内填充(内边距)：边框与内容之间的距离

- content

> 内容

##### 具体用法

> margin-top   margin-right   margin-left   margin-bottom

-   margin:50px;(上 右 下 左)
-   margin:50px 100px;(上下 左右)
-   margin:0 anto;    (子元素在父元素中水平居中)
-   margin:50px 100px 150px;(上 左右 下)
-   margin:50px 100px 150px 200px(上 右 下 左)

> border的用法

```css
border：1px solid red
border-top\border-right\border-bottom\border-right
```

##### 元素的实际高度

> 实际宽度 = border-left+padding-left+width+padding-right+border-right;
>
> 实际高度 = border-top+padding-top+height+padding-bottom+border-bottom

##### 盒子模型的问题 

- 大部分元素的margin padding 默认为0，但是有一部分元素的margin padding不为0---> body  h1~h6  段落标签 列表标签
- 相邻的两个块元素的margin会重合。值会取最大值。
- margin可以设置负数，padding不可以
- 行内元素的margin只有左右没有上下

- 子元素撑不开父元素的原因

  - 两个发生嵌套关系的元素
  - 父元素没有上边框
  - 父元素没有设置上padding值
  - 父元素与子元素之间没有内容，此时子元素margin-top会作用到父元素身上

  ```css
  解决方法：
  <1>用父元素的padding-top值代替子元素margin-top值
  <2>给父元素添加overflow：hidden
  ```

#### CSS中的定位

> 定位的元素脱离文档层，到达定位层，元素被定位后可设置5个属性值
>
> top   left   right   bottom   z-index

- 相对定位

> 相对于自身来定位，在文档层中保留原来的位置

```css
postion: relative;
```

- 绝对定位

> 相对于最近的、已定位的祖先元素，完全脱离文档流

```css
position: absolute;
```

- 固定定位

> 相对于浏览器的四条边定位，完全脱离文档流

```css
position: fixed;
```

##### Float(浮动)及其引发的问题

> 文档流：标准情况下页面元素从左往右、从上到下依次排列
>
> 浮动的原理：让元素脱离文档流，让元素从文档层浮动到浮动层

###### 浮动引发的问题：浮动的子元素撑不开父元素。

- 给父元素添加 overflow:hidden (超出部分隐藏)
- 在父元素内容最后添加拥有清除浮动属性的元素。clear : ; (属性值：right left both)  #清除左/右元素对此元素的浮动影响

##### CSS中常用的几种居中方式

- 水平居中

```css
left: 50%;
margin-left: -(width*0.5);
```

- 垂直居中

```css
top: 50%;
margin-top: -(top*0.5);
```

- 绝对居中

```css
left: 50%;
margin-left: -(width*0.5);
top: 50%;
margin-top: -(top*0.5);
```

- 水平居中

```css
left:：0;
right：0;
margin： 0 auto；
```

- 垂直居中

```css
bottom： 0；
top：0
margin：0 auto；
```

- 绝对居中

```css
left:：0;
right： 0;
bottom： 0；
top：0
margin：auto auto；
```

### Flex布局

#### 容器的属性：

- flex-direction:  决定主轴方向
  - row   主轴在水平方向，从左往右
  - row-reverse  主轴在水平方向，从右往左
  - column   主轴在垂直方向，从上往下
  - column-reverse   主轴在垂直方向，从下往上
- flex-wrap:  决定项目换行
  - wrap  项目换行
  - nowrap  项目不换行(默认)
  - wrap-reverse：项目换行，第一行在下方
- justify-content:   决定项目在主轴上的对齐方式
  - flex-start  主轴的起点
  - flex-end  主轴的终点
  - center  主轴的中心
  - space-between  两端对齐，项目之间的间隔都相等
  - space-around  每个项目两侧的间隔相等，项目之间的间隔比项目与边框的间隔大一倍。 
- align-items：定义项目在交叉轴上的对齐方式（适用于一根轴线）
  - flex-start  交叉轴的起点对齐。 
  - flex-end  交叉轴的终点对齐。 
  - center  交叉轴的中点对齐。 
  - baseline  项目的第一行文字的基线对齐。 
- align-content:定义项目在交叉轴上的对齐方式 （适用于多根轴线）
  - flex-start  交叉轴的起点
  - flex-end  交叉轴的终点
  - center  交叉轴中心
  - space-around  每根轴线两侧的间隔都相等，轴线之间的间隔比轴线与边框的间隔大一倍。 
  - space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。

#### 项目的属性：

- order:  属性定义项目的排列次序。数值越小，排列越靠前，默认为0。 
- flex-grow:  属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。 
- flex-shrink:  属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小;值为0时，空间不足，项目也不缩小 。
- flex-basis:  定义项目占据的主轴空间。
- flex:  
- align-self:  定义单个项目在交叉轴上的对齐方式
  - flex-start  交叉轴起点
  - flex-end  交叉轴终点
  - center  中心

### 文本模型

- 文本换行

```css
word-break: break-all;           #  使非中日韩文本换行
```

- 单行文本溢出处理

```css
white-space: nowrap;       #   禁止换行
overflow: hidden;
text-overflow: ellipsis;    #   文本超出部分以省略号显示
```

- 多行文本溢出处理

```css
display: -webkit-box;          //指定为弹性盒子
-webkit-box-orient: vertical;          //在弹性盒模型中指定元素的排布顺序
-webkit-line-clamp: number;              //设置几行文本后溢出
line-height: npx;                       //与height成倍数关系
overflow: hidden;
```

### 浏览器内核

  ```html
-webkit-   # Chrome浏览器
-moz-      # firefox浏览器
-ms-       # IE浏览器
-o-        # opera浏览器
  ```

### 移动端布局步骤

> 视口：视觉视口   布局视口   理想视口

- 修改视口

  ```css
  <meta name="viewport" content"width=device-width">
  ```

- 引入rem.js  实现适配

  > em      当前字体的倍率   
  >
  > rem     html字体的倍率

  ```css
  <script src="js/rem.js" type="text/javascript"></script>
  ```

- 修改rem.js中设计稿的宽度
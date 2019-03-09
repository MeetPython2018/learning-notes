### DOM(文档对象模型)

#### 获取元素

- getElementById() 方法

> getElementById() 方法返回带有指定 ID 的元素 

```js
let box = document.getElementsById("idNName");
```

- getElementsByClassName() 方法

> 查找带有相同类名的所有 HTML 元素

```js
let box = document.getElementsByClassName("intro");
# 上面的例子返回包含 class="intro" 的所有元素的一个列表：
```

- getElementsByTagName() 方法

> getElementsByTagName() 返回带有指定标签名的所有元素 

```js
let box = document.getElementsByTagName("TagName");
```

- 在指定范围内获取元素

```js
let box = obj.getElementsByClassName("banner");
```

- 获取选择器中的第一个元素

```js
let obj = document.querySelector("queryName");
```

- 获取选择器选中的集合(通过下标以遍历的方式访问)

```js
let obj = document.querySelectorAll("queryName");
```

#### 操作属性

##### 标准属性

> obj.attr

##### 自定义属性

- 获取属性

```js
obj.getAttribute(name);
```

- 设置属性

```js
obj.setAttribute(name,value);
```

#### 操作样式

##### 获取元素的样式

- 行内样式

```js
obj.style.attr
```

- css样式

```js
getComputedStyle(obj,null).attr
```

##### 设置元素的样式

- 行内样式

```js
obj.style.样式名=样式值;
```

- 批量设置样式

```js
obj.className = '';
obj.calssList.add("");       # 添加类
obj.calssList.remove("");    # 移除类
obj.calssList.toggle("");    # 切换类
obj.id='searchBox';
```

#### 操作内容

> 改变 HTML 内容

- obj.innerText;         #设置元素的内容
- obj.innerHTML;      #设置元素的内容，可以设别标签对

#### 元素的物理属性

##### 元素的大小及位置

- obj.offsetwidth:     获取元素的真实宽度（width+padding+border）

- obj.offsetHeight:     获取元素的真实高度

- obj.offsetTop:        获取当前元素到有定位父元素的垂直偏移量

- obj.offsetLeft:        获取当前元素到有定位父元素的水平偏移量

- obj.scrollTop:   有滚动条的元素，浏览器滚动时在垂直方向的拉伸距离

- obj.scrollLeft:     有滚动条的元素，浏览器滚动时在水平方向的拉伸距离

  ```js
  document.body.scrollTop||document.documentElement.scrollTop
  ```

##### 添加元素

1.动态创建元素

> 如需向 HTML DOM 添加新元素，您首先必须创建该元素，然后把它追加到已有的元素上。 

```js
document.creatElement("TagName");
```

2.添加类名

```js
obj.className="";
```

3.插入到页面

```js
父元素.appendChild(子元素)
document.body.appendChild(div);
```

### BOM(浏览器对象模型)

> BOM提供了独立于内容 而与浏览器窗口进行交互的对象；
>
> 由于BOM主要用于管理窗口与窗口之间的通讯，因此其核心对象是window；
>
> BOM由一系列相关的对象构成，并且每个对象都提供了很多方法与属性；

```js
移动、调整浏览器大小的window对象
用于导航的location对象与history对象
使用document作为访问HTML文档的入口，管理框架的frames对象
获取浏览器、操作系统与用户屏幕信息的navigator与screen对象
```

#### window对象：

> 移动、调整浏览器窗口的大小 

##### 属性：

- 浏览器宽高
  - window.innerheight   获取浏览器的高度
  - window.innerWidth   获取浏览器的宽度
  - document.documentElement.clientWidth      获取浏览器的宽度
  - document.documentElement.clientheight      获取浏览器的高度
- 浏览器左上角距屏幕左上角的偏移量
  - window.screenTop    垂直偏移量
  - window.screenLeft    水平偏移量

##### 方法：

- alert()     弹出框
- prompt()    输入框
- confirm()       弹出选择框
- close()    关闭页面
- open()    打开页面       括号里的参数：url,
- setInterval(function,1000)    隔一段时间(ms)重复不断地执行函数
- clearInterval(t)     清除时间函数
- setTimeout(fn,1000)      隔一定的时间只执行一次函数
- clearTimeout(t)            清除时间函数      

##### 获取表单的值：obj.value

#### history对象：

##### 属性：

- history.length    用来显示历史纪录的长度

##### 方法：

- history.forward()   前进
- history.back()      后退
- history.go(0)   刷新

#### location对象：

##### 属性：

- location.href    设置或获取页面地址
- location.host    主机名加端口号
- location.hostname    主机名
- location.port      端口号
- location.protocol   协议
- location.pathname   路径
- location.search     问号后的搜索字段

##### 方法：

- located.reload()    重新加载
- location.replace("history.html")    页面替换，不会增加历史纪录
- location.assign("history.html")     页面替换，能够增加历史纪录
### 事件添加方式

- 节点.onclick=function(){}

- 节点.addEventListener("事件",事件处理程序,[事件类型])；

### 事件的构成

- 事件源：谁去触发事件，谁就是事件源
- 事件：  如点击事件，鼠标移入、移出事件
- 事件处理程序

### 常用事件

#### web端鼠标事件：

- onclick                        单击
- ondblclick                   双击
- onmousedown          按下
- onmouseup               抬起
- onmousemove          鼠标移动
- onmouseover            鼠标移入
- onmouseout              鼠标移出
- onmouseenter          鼠标移入
- onmuseleave             鼠标移出
- onmousewhell

##### 鼠标事件对象常用方法：

- clientX      距浏览器的X轴偏移量
- clientY       距浏览器的Y轴偏移量
- offsetX      距事件源X轴偏移量
- offsetY       距事件源Y轴偏移量
- screenX     距离屏幕X轴偏移量
- screenY      距离屏幕Y轴偏移量

#### 屏蔽浏览器默认样式

```js
document.oncontextmenu=function(e){
        e.preventDefault();
    }
```

#### 键盘事件

- onkeydown    键盘按下
- onkeyup        键盘抬起
- onkeypress    键盘按下(当按下系统功能键shift alt delete ctrl等时不会触发)

##### 键盘事件对象常用属性：

- keyCode    键盘码
- ctrlKey    是否按下Ctrl
- shiftKey     是否按下Shift
- altKey        是否按下Alt
- key       键盘名

#### 移动端事件：

- ontouchstart
- ontouchmove
- ontouchend

### 表单事件

- oninput      输入
- onchange      内容发生改变，并且失去焦点
- onfocus      获取焦点
- onblur        失去焦点
- onsubmit      提交表单
- onselect   文本选中

### 事件流

> 当触发一个事件时，由这个事件的容器到整个文档都按照特定的顺序进行依次的触发

### 事件的分类

#### 捕获型事件：true

> 从不具体的事件源到具体的事件源

#### 冒泡型事件：false

> 从具体的事件源到不具体的事件源

### 阻止事件流

```js
let event = event || window.event
event.stopProagation();
event.returnValue=true;
```

### 事件委派

event.target        目标事件源

### 事件对象：用来保存事件触发时的信息

W3C在    事件处理程序的形参中

IE在      window.event
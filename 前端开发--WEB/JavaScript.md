### JavaScript

> JavaScript是一种直译式脚本语言，是一种动态类型、弱类型、基于原型的语言，内置支持类型。它的解释器被称为JavaScript引擎，为浏览器的一部分，广泛用于客户端的脚本语言，最早是在[HTML](https://baike.baidu.com/item/HTML)（标准通用标记语言下的一个应用）网页上使用，用来给HTML网页增加动态功能。 

#### 引入js

> js的几种引入方式是互相关联的，可以互相操作和访问
>
> 外部js中不能有<script>标签对
>
> 嵌入式js中不能添加src属性

- 外链式

```html
<script src='index.js'></script>
```

- 嵌入式

```html
<script>
	alert('hello world!')
</script>
```

- 事件后

```html
<button onclick='alert(123)'></button>
```

#### js中的调试工具

- 弹出框

```js
alter(123);
```

- 输出到控制台

```js
console.log('123');
```

- 输出到页面中(可以识别标签对)

```js
document.write("a");
document.write("<h3>这是H3级标题</h3>")
```

- 输入框

```js
prompt("请输入:")
```


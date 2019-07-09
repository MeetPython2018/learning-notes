- 创建虚拟环境

```python
python3 -m venv myvenv
```

- 进入/退出虚拟环境

```python
cd venv/Script 
activate
source ./activate         #进入虚拟环境
deactivate               #退出虚拟环境
```

- 升级pip并安装工程所需要的包

```python
pip install -U
pip install Flask
pip install pymysql
```

#### Flask的用法

```python
from flask import Flask,rerender_template

app = Flask(__name__)     
@app.route("/")        #route()装饰器告诉Flask应该触发我们的函数的URL
def hello():                      #返回我们想要在用户的浏览器中显示的消息
    return "hello,world!"
@app.route("/login")
def login():                        #必须先新建一个templates包来存放渲染的模板
    return render_template("index.html")
```

##### 请求HTTP

```python
from flask import request

@app.route('/login', methods=['GET', 'POST'])  #装饰器的methods参数处理不同的HTTP方法。
def login():
    if request.method == 'POST':
        return do_the_login()
    else:
        return show_the_login_form()
```

#### PyMySQL的操作

```python
#!/usr/bin/python3
 
import pymysql
 
# 打开数据库连接
db = pymysql.connect("localhost","testuser","test123","TESTDB" )
 
# 使用 cursor() 方法创建一个游标对象 cursor
cursor = db.cursor()
 
# 使用 execute()  方法执行 SQL 查询
cursor.execute("SELECT VERSION()")
 
# 使用 fetchone() 方法获取单条数据.
data = cursor.fetchone()
 
print ("Database version : %s " % data)
 
# 关闭数据库连接
db.close()
```

##### 数据库查询操作

> Python查询Mysql使用 fetchone() 方法获取单条数据, 使用fetchall() 方法获取多条数据。

- fetchone()                       //该方法获取下一个查询结果集。结果集是一个对象
- fetchall()                          //接收全部的返回结果行
- rowcount                         //这是一个只读属性，并返回执行execute()方法后影响的行数。

#### 连接数据库

```python
import pymysql
db = pymysql.connect(
    host="localhost",
    user="root",
    passwd="passwd",
    db="databasename",
    charset="utf8",
    cursorclass=pymysql.cursors.DictCursor)
```

#### 架构

BS架构   

> B/S架构即浏览器和[服务器](https://baike.baidu.com/item/%E6%9C%8D%E5%8A%A1%E5%99%A8)架构模式 

可以随时访问最新的内容，免去用户下载；有延迟不能够流畅的操作，体验性不好

CS架构  

>   Client/Server架构，即客户端/服务器架构 

延迟低；依赖硬件，必须得有客户端，更新不及时

#### ajax   （asjnc javascript and  xml    利用JavaScript异步能力处理数据） 

要解决的问题：

1.页面无刷新操作数据

2.按需获取问题

3.让基于B/S架构的软件能够C/S软件一样，流畅加载

> 优点：减轻服务器的负担、按需取数据、最大程度的减少冗余请求、局部刷新页面,减少用户心理和实际的等待时间,带来更好的用户体验、基于xml标准化,、并被广泛支持,不需安装插件 

```js
var ajax = new XMLHttpRequest()         #创建ajax对象
ajax.onreadystatechange=function(){
    console.log(ajax.readystate)     1:收到请求  2:出发  3：找到  4：拿到数据
}
ajax.onload=function(){
    ajax.responseType=""
}
ajax.open("get/post","2.html")
ajax.send()
```

html树形结构---->模板        数据库---->模型

5.可以处理多种类型的数据     (text   json   blod   arraybuffer)

```js
json.dumps(result)
    sucess:function(){
        for (var i=0;i<data.length;i++){
            tr=document.cearteElment("tr")
            tds=`<td>${data[i]["id"]}</td>`
        }

```

下载send_from_

url   统一资源定位符

git://[用户名：密码@]主机：端口/路径/文件名？查询字符串#锚链接

https://username:123@baidu.com:80/aa/aa

```js
location.hash
documnet.querSelector("input")
var ajax=XMLHttpRequest()
ajax.onload=function(){
    
}
ajax.open()
ajax.send()
```


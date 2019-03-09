### Linux

> Linux是一套免费使用和自由传播的[类Unix](https://baike.baidu.com/item/%E7%B1%BBUnix)[操作系统](https://baike.baidu.com/item/%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/192)，是一个基于[POSIX](https://baike.baidu.com/item/POSIX)和[UNIX](https://baike.baidu.com/item/UNIX)的多用户、[多任务](https://baike.baidu.com/item/%E5%A4%9A%E4%BB%BB%E5%8A%A1/1011764)、支持[多线程](https://baike.baidu.com/item/%E5%A4%9A%E7%BA%BF%E7%A8%8B/1190404)和多[CPU](https://baike.baidu.com/item/CPU)的操作系统。 

### 浏览器的功能

1. 呈现内容        解析内容和样式     -webkit-   -ms-    -mos-   -o-
2. 实现交互逻辑       js的V8引擎
3. 进行数据传递          chorme  net引擎

### 命令窗口大小设置快捷键操作

shift+crtl+"+"

ctrl+"-"

ifconfig  查看ip地址

### 重要指令：

```markdown
sudo su         # 以root用户运行
sudo passwd     # 以管理员登录时可以重置密码
```

### 文件结构

**/bin   重要的二进制应用程序**

**/boot   启动配置文件**

**/dev    设备文件**

**/etc    配置文件，启动脚本**

**/home    本地用户主目录**

**/lib    系统库文件**

**/lost+found       系统临时文件夹**

**/media   挂载可移动介质**

**/mnt     挂载文件系统**

**/opt     提供一个供可选的应用程序安装目录**

**/proc    特殊的动态目录**

**/root     root用户主文件夹**

**/sbin    超级管理员可以运行的内容**

**/sys   和proc一样**

**/tmp    临时文件夹**

**/usr      关于用户自己的配置文件**

**/var     经常变化的文件**

### 命令

#### cd 切换目录

cd / 切换到根目录   

cd .. 退到上级目录

cd -     回到最近进过的目录

#### clear    清空屏幕

#### 帮助

ls --help   查看帮助

man ls      查看帮助

#### ls 查看目录下的文件

ls -a    显示当前目录的所有文件，包含系统目录

ls -l      文件的详细信息

#### which    查找文件对应的目录

#### pwd   当前所在目录

#### history查看最近使用过的所有命令，history  -c   清除最近使用过的Linux命令

### 操作文件

#### 创建文件

echo                                      #  输出内容

echo   123 >  1.txt                   #  向1.txt里写入内容123

echo    456 >>  1.txt                     #  向1.txt里追加内容456

gedit 1.txt                                #  用编辑器打开1.txt

cat 1.txt                            #  预览文件内容

touch 2.txt                  #  直接创建一个文件(文件存在则不会创建)

vi/vim  3.txt            #  创建一个文件

```markdown
正常模式（按Esc或Ctrl+[进入） 左下角显示文件名或为空
插入模式（按i键进入） 左下角显示--INSERT--
```

#### 操作文件/文件夹

mkdir  目录名        #创建一个目录

mkdir -p a/b/c               #创建层级目录

rm   文件名			    #删除文件

rm   *.文件类型                        #删除同一类型文件

rm  -rf   目录名                  #删除该目录下的所有文件及子文件夹

rmdir  目录名                #只能删除空目录

rmdir -p a/b/c             #连续删除空的层级目录

mv   a  aa            #给a重命名为aa

mv    aaa    document          #将aaa移动到document中

cp a b              #在当前目录下拷贝一个文件a的副本文件b

cp a -r b                #在当前目录下拷贝一个文件夹a的副本文件夹b

#### find   路径   查找文件

获取操作权限  sudo find ngi*       #查找文件

grep 内容  路径      #在指定路径中查找内容

### 管道：|

> ####  ps -aux | grep 3515

### 链接

ln -s 源文件  目标文件               **#软链接**   几乎不占磁盘空间，相当于做了一个镜像

ln   源文件    目标文件              **#硬链接**，相当于拷贝了一份文件    ！只能做文件的快捷方式不能做文件夹的快捷方式

rm -rf 目标          #清除链接

### 文件的解压缩

> 压缩的前提得先打包文件   

-z  压缩格式    gzip     -j  压缩格式  bz2

tar -cvf  目标文件  源文件    (target -creatviewfile)           #打包

tar -xvf   源文件  -C   目标文件                                 #解包到指定目录

tar -zcvf   目标文件   源文件                                                                        #gzip压缩

tar -zxvf  源文件 -C 目标文件                                                              #解压到指定目录          

-  zip压缩

```py
zip dest source
```

- unzip(-d)(path) 解压

```py
unzip dest
```

### 磁盘管理

df (选项)(参数)            #查看磁盘的使用情况

df -h                           #查看磁盘的使用情况(易读版)

du  (选项)(参数)         #查看当前目录的内容存储情况

### 文件传输

> ssh文件传输协议    (secure shell)        

sudo apt-get install openssh-server      #开启Ubuntu的连接权限

#### 上传文件命令格式：

scp  local_folder remote_username@remote_ip:remote_folder        给服务器上传文件

scp -r local_folder remote_username@remote_ip:remote_folder        给服务器上传文件夹

#### 下载文件：

scp   remote_username@remote_ip:源文件路径  目标文件路径            从服务器download文件

scp   -r remote_username@remote_ip:源文件路径   目标文件路径           从服务器download文件夹

### 网络通讯

- ifconfig 查看或设置网卡

改ip地址:  sudo ifconfig eth0 修改后的IP

### 网络传输协议

- TCP协议   传输控制协议

- UDP协议   用户数据报协议

### 端口

netstat  -aup    查看UDP端口号的使用情况

netstat  atp	   查看TCP端口号的使用情况

### 软件的安装和管理

#### 1.apt-get方式安装

- 添加包的地址
  - sudo add-apt-repository ppa:webupd8team/python3.6
- 删除软件包(不推荐)
  - sudo apt-get remove packagename
- 删除软件包包括配置文件(推荐使用)
  - apt-get --purge remove mysql-server mysql-client
- 删除该软件的依赖包
  - apt-get autoremove mysql-server mysql-client
- 清理无用的包
  - sudo apt-get clearn && sudo apt-get autoclean     清理无用的包   &&同时运行两个命令

- 获取新的软件包列表

```py
sudo apt-get update
```

#### 2.源码安装

```py
wget url     # 下载源码
tar -zxvf sourcename    # 解压源码
```

- 找到configer,并执行以下文件

```py
配置configrue,
./configure --prefix=/opt/python3.7   [--enable-optimizations]
```

```c
sudo make all    # 编译
sudo make install    # 安装
```

- 多版本共存

```python
sudo update-alternatives --install /usr/bin/python3 python3 /opt/python3.7/bin/python3.7 500
update-alternatives --install link name path priority    [--slave link]
其中link为系统中
```

### 设备操作

- 关机

```py
$ halt   立刻关机
$ poweroff    立刻关机
$ shutdown -h now   立刻关机（root用户使用）
$ shutdown -h 10    10分钟后关机
```

- 重启

```py
$ reboot
$ shutdown -r now
$ shutdown -r now 10
$ shutdown -r 20:15
$ shutdown -c 取消重启
```

- 进程

```py
ps -aux           # 显示所有包含使用者的进程
top             # 动态显示所有进程
kill pid          # 杀死进程   pid是进程号
kill -9 pid       # 强制杀死进程     使用次命令都杀不掉的进程为守护进程
守护者进程在：  cd /etc/init.d/
	sudo /etc/init.d/mysql stop   停止守护进程
	sudo /etc/init.d/mysql start   开启守护进程
	sudo /etc/init.d/mysql restart   重启守护进程
```

### 权限管理

重启按shift进入高级模式 在root单命令下添加sudo

- 查看用户/组

```python
whoami                        #查看当前在线的用户
who                   #查看所有在线的用户
cat /etc/passwd               #查看用户是否创建成功
cat /etc/group                #查看组
groups  用户名        #查看该用户属于那个组   主组  副组
```

- 关于用户的操作

```python
su  可用来切换用户
sudo useradd -m 用户名         #创建用户
sudo passwd 用户名        #设置密码
sudo userdel -f 用户名         #删除用户
sudo usermod 用户名 -d /home/first/demo     #修改登录目录
sudo useradd 用户名 -g 组名             #创建一个用户并将其添加到已经存在的组里
```

- 组的操作

```python
sudo groupadd 组名           #创建组
sudo groupmod 源名 -n 目标名        #改组名
sudo groupdel 组名           #删除组
sudo usermod 用户名 -g 组名        #将用户添加到组里  
sudo usermod 用户名 -G 组名        #将用户追加到组里
sudo gpasswd -a 用户名 组名        #给组里添加用户
sudo gpasswd -d 用户名 组名        #在组删除用户
usermod -a -G sudo username       #让创建的用户也有sudo权限
usermod -a -G adm username        #让创建的用户也有adm权限
```

##### chown  更改文件的所有者

chown -R 用户名:组名 aaa

##### chmod  更改文件的权限

sudo chmod  u=rwx，g=rwx，o=rwx  文件名

sudo chmod   777   文件名                                #该文件对所有用户都开放权限

1->x        2->w      4->r       7代表：rwx    6代表：rw     5代表：rx     3代表：wx

```py
#!/usr/bin/env python           //自动执行python
./demo.py       执行demo.py文件
```

### 开发

```python
ctrl+z  后台挂起运行
fg %1   调用
```


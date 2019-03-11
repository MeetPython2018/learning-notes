## MySQL  关系型数据库

> 数据库（Database）是按照数据结构来存储和管理数据的查看， 所有的关系型数据库，是建立在关系模型基基上的数据库，借助于集合代数等数学概念和方法来管理数据库中的数据。 
>

### 进入数据库

    mysql -hlocalhost -u root -p

### MySQL常用命令

#### 创建数据库

```mysql
create database dbname charset utf8;           #创建新数据库（可以指定字符集）
use databasename;                #进入数据库
drop database databasename;            #直接删除数据库
show tables;                          #查看当前数据库下的表
select version(),current_date;        #当前mysql版本和当前日期
select database();               #查看当前所在数据库
```
#### 创建表(示例)

```mysql
create table stu(
    id int(10) auto_increment primary key,
    name varchar(255),
    age varchar(10),
    sex varchar(10))default charset=utf8;
```
#### 操作表中的数据

```mysql
desc tablename;      #查看表的结构 describe
insert into tablename (name,sex,age) values("知道",'男','20');    #向表中插入数据
select * from tablename;                   #查询表中的所有数据
select * from category,category_info where category.cid=category_info.cid    #关联查询
select * from category inner join category_info on category.cid=category_info.cid   #内联查询
update tablename set filed=val where id=1;       #更新表中的某条数据  filed字段
delete from tablename where id=2;               #删除表中的某条数据
truncate tablename;                  #清空表中的数据         
drop table tablename;                           #删除表
```
pip uninstall  包名     通过pip卸载包

    #    mysql里的注入
    --   mysql里的注入
    sql注入
    " or 1=1; -- 

#### hash加密

md5=hashlib(b'')

md5.update()

```mysql
-- 高级查询
select * from logs where phone in (select phone from students where classid in (select id from classes where fid in (select cid from category where cid=9)))             -- 子查询

cursor.execute(select logs.*,students.name as sname,classes.name as cname from logs left join students on logs.phone=students.phone left join classes on students.classid=classes.id where logs.phone in(select phone from students where classid in (select id from classes where fid in(10))) and date format(lods.time,'%Y-%m-%d')='2018-11-13')
```

## MySQL数据库

### DCL (Data Control Language) 数据库控制语言

#### 命令行链接方式

> MySQL -u用户名 -p密码 -h 服务器IP地址 -P 服务器端MySQL端口号 -D 数据库名
>

#### 用户管理

##### 创建本地用户

```mysql
-- 进入mysql数据库
use mysql;
-- 创建本地用户
create user 'user_name'@'localhost' identified by 'password';
-- 刷新MySQL的系统权限相关表，使添加用户操作生效，以免会出现拒绝登录
flush privileges;
```

##### 创建远程用户

```mysql
-- 从192.168.122.12登录的用户
create user 'user_name'@'192.168.122.12' identified by 'password';
-- 从任意ip登录的用户
create user 'user_name'@'%' identified by 'iamsuperboy';
-- 不做指定默认为'%'
create user 'user_name' identified by 'iamsuperboy';
```

##### 用户的基本操作

```mysql
-- 1.修改密码
use mysql；
ALTER USER 'caoyao'@'localhost' IDENTIFIED WITH mysql_native_password BY '201811';
-- update mysql.user set password=password('新密码') where user='user_name';
flush privileges;
-- 2.用mysqladmin修改密码
mysqladmin -u用户名 -p旧密码 password 新密码;
-- 查看用户权限
SHOW GRANTS FOR 'user_name'@'localhost';
-- 修改用户的权限
grant all privileges on databasename.* to 'user_name'@'localhost';
# all 可以替换为  select,delete,update,create,drop
-- 赋予部分权限
grant select,delete,update,insert on 数据库/表.* to user_name@'localhost';
-- 赋予所有权限
grant all privileges on 数据库.* to user_name@localhost identified by 'password';
-- 删除用户
delete FROM mysql.user Where user='user_name' and host='localhost';
-- 查看当前登录用户
select user();
```

##### 忘记root密码

- 关闭正在运行的mysql服务
- 进入mysql安装目录
- 运行下面的命令  
      mysql --skip-grant-tables
- 再开一个命令窗口，转到mysql/bin

##### 允许远程链接

```mysql
grant all privileges on *.* to 'root'@'%' identified by '154303' with grant option;
flush privileyes;
```

##### REVOKE语句

```mysql
-- 撤销update权限
revoke update on databasename.* from user_name@localhost;
-- 撤销所有权限
revoke all on databasename.* from user_name@localhost;
```

#### 数据库及表管理

##### 用来备份数据库

```mysql
-- 备份数据库的所有数据
mysqldump -u [uaer_name] -p[password] [databases_name] > dumps.sql；
-- 只备份数据库的结构
mysqldump -u [uaer_name] -p[password] --no-data [databases_name] > dumps.sql；
-- 只备份mysql数据库的数据
mysqldump -u [uaer_name] -p[password] --no-create-info [databases_name] > dumps.sql；
-- 导出多个数据库
mysqldump -u [uaer_name] -p[password] [dbname1,dbname2,...] > [all_dbs_dump_file.sql]；
mysqldump -u [uaer_name] -p[password] --all-databases > [all_dbs_dump_file.sql]；
```

##### 查看表信息

```mysql
SHOW COLUMNS FROM teach like expression；
SHOW COLUMNS FROM teach where field='字段名'；
```

##### 表的优化操作

```mysql
ANALYZE TABLE table_name;    -- 分析表语句
OPTIMIZE TABLE table_name;   -- 优化表语句
CHECK TABLE table_name;      -- 检查表语句
REPAIR TABLE table_name;     -- 修复表语句
```

### DDL(Data Defined Language)(数据库模式定义语言)

#### 创建/删除数据库

```mysql
create database IF NOT EXISTS 数据库名; -- IF NOT EXISTS  若数据库不存在时才创建
drop database IF EXISTS 数据库名;       -- IF EXISTS  数据库存在时才删除
```

##### 创建表

```mysql
mysql> create table if not exists student(                 -- 创 建 表 示 例
    -> id int(16) auto_increment,
    -> sex enum('1','0') NOT NULL,                         -- 枚举型，必选其一
    -> phone varchar(11) unique,                           -- 该字段存储的数据不可重复
    -> password varchar(32),
    -> hobby set('以前','现在','以后'),
    -> primary key (id))engine=InnoDB default charset=utf8;
```

##### 编辑表信息

```mysql
SHOW CREATE TABLE table_name            -- 查看表信息
ALTER TABLE 'table_name' CHANGE [COLUMN] oldname newname vachar(100);    -- 修改表信息
ALTER TABLE 'table_name' ADD [COLUMN] field_name enum('','') not null [AFTER field_name];    -- 向表中追加字段   AFTER filedname 追加在指定的字段后面
ALTER TABLE 'table_name' DROP field_name;                   -- 删除表中的一列
ALTER TABLE 'table_name' ADD PRIMARY KEY(primary_key_name)   -- 添加主键
ALTER TABLE 'table_name' ADD UNIQUE (column_name)     -- 添加唯一索引
ALTER TABLE 'table_name' ADD FULLTEXT (column_name)   -- 添加全文索引
ALTER TABLE 'table_name' ADD INDEX (column_name)      -- 添加普通索引
ALTER TABLE 'table_name' drop index column_name            -- 删除普通索引
ALTER TABLE 'table_name' ENGINE = InnoDB                  -- 修改引擎
show ENGINEs     -- 查看MySQL支持的引擎  
```

#### 数据类型

##### 整型

```mysql
zerofill？  数据前面的位数是否需要零填充？
显示宽度？  是否需要将数据?型??的位数用0表示出来
```

##### 字符串类型

char 定长    0--255字节        varchar  不定长   0-65535字节         text 短文本

##### 日期类型

DATE 日期	    DATETIME  混合日期和时间		TIMESTAMP  时间戳

##### 数据库引擎

MyISAM

> .frm (存储定义)    MYD(存储数据)     MYI(存储索引)
>

InnoDB

> InnoDB是一个健壮的事务型存储引擎，数据存储引擎已被很多互联网公司使用。
>

##### 索引类型

###### mysql外键

> 定义一个副表的非主键字段和主表的主键关联时，那么这个非主键字段叫做是外键

- 外键有什么用
  - 如果在副表当中添加一个主表里面不存在的数据，插入操作会报错

  - 如果在主表当中进行修改或者删除操作时，当副表里面有关联的数据，那么主表会阻止执行

  - 创建外键

      ```mysql
      field_name int(10),
      CONSTRAINT constraint_name FOREIGN KEY (field_name) 
      REFERENCES parent_class(field_name))default charset=utf8;
      ```

- 添加外键

    ```mysql
    -- action -> district(默认) cascade(关联) set null(将关联的数据设为null) no action(什么也不做)
    ALTER TABLE table_name ADD FOREIGN KEY (field_name)
    REFERENCES parents_table(field_name)
    ON DELETE action 
    ON UPDATE action
    ```

- 移除外键

    ```mysql
    ALTER TABLE table_name
    DROP FOREIGN KEY constraint_name;       -- 移除外键
    alter table stu drop key keyname;       -- 移除key值
    ```

### DML（Data Manipulation Language）数据库操作语言

#### INSERT

> 具有select子句的表（快速拷贝一个表）
>

```mysql
create table new_table like old_table;                     -- 表结构的拷贝
insert into new_tablename select * from old_tablename;     -- 表数据的拷贝

insert into table_name (filed,...) values(值1,...) ON DUPLICATE KEY UPDATE action   -- 理
```

#### REPLACE

```mysql
replace into table_name (filed1,...) values(值1,...);     -- 插入的信息已存在，并且?、配置了unique,??更新
```

#### UPDATE语句简介

```mysql
UPDATE [LOW_priority] [IGNORE] table_name set column_name1=value where
```

##### 带有select子句的更新

```mysql
select * from teacher order by rand() limit 1;     -- 随机查询出一条数据
update stu set sname=(select tname from teach order by rand() limit 1) where tname is null;     -- 随机查询出一条数据更新
```

##### 关联更新

```mysql
update table1,table2...
set table.attr=val,table.attr=val...
where condition;
```

##### 删除语句

```mysql
delete table1,table2 from table1 inner join table2 on ...        -- 关联删除
truncate table_name;                                   -- 清空表，自增值也清空
```

#### 日志管理

##### 日志种类

###### 错误日志

```mysql
show global variables like '%log_error%';        # 查看错误日志的存储位置
```

###### 一般查询日志

```mysql
show global variables like 'general_log';   # 查看一般查询日志的存储位置
```

###### 慢查询日志

```mysql
查询超时：long_query_time
启动慢查询日志：log_slow_queires={YES|NO}
启动慢查日志：slow_query_log
日志纪录文件：slow_query_log_file={file_name}
```

###### 二进制日志

###### 中继日志

###### 事务日志

> 事务性存储引擎用于保证（ACID）原子性、一致性、隔离性和持久性；其不会立即写到数据文件中，而是写到事务文件中

```mysql

```

##### MySQL全局变量查询与修改

###### 查询变量

```mysql
show global variables like '%log%';   -- % 用于模糊查询    _ 模糊查询前面只能有一个任意字符
```

###### 修改变量

```mysql
set global variable_name=val
```

## DQL（Data Query Language）数据查询语言

### 基础语法

```mysql
-- 标准语法
SELECT column_1,column_2...
FROM 
	table_1
[inner] [left]
where
	conditions
GROUP BY column_1
HAVING group_conditions
ORDER BY column_1
LIMIT offset
```

##### 别名

> 当字段名过长时用AS起个别名

### 操作符

| 操作符   | 描述                             |
| -------- | -------------------------------- |
| =        | 等于，几乎任何数据类型都能使用它 |
| <> 或！= | 不等于                           |
| <        | 小于                             |
| >        | 大于                             |
| <=       | 小于等于                         |
| >=       | 大于等于                         |
| or       | 或者                             |
| and      | 且                               |
| not      | 非                               |

### 运算符

##### BETWEEN运算符

> BETWEEN运算符允许指定要测试的值范围

```mysql
SELECT * FROM table_name field_name [NOT] BETWEEN begin_expr AND end_expr;
BETWEEN CAST('1997-03-08', AS DATE) AND CAST('2018-03-08', AS DATE);       -- 时间区间
select * from table_name where field_name like '%老￥%师%' ESCAPE '$';
```

##### IN操作符

```mysql
select * from table_name where birth in ("vlues1","vlues1",..);
```

##### find_in_set函数

> SQLFIND_IN_SET()函数

```mysql
select * from teach where find_in_set('values',filed)
```

##### GROUP BY

> group by子句通过列或者表达式的值将一组行分组为一个小分组的汇总纪录，group by 子句为每个分组返回一行

```mysql
SELECT 
	c1,c2,..... aggregate_function(ci)
FROM
	table
WHERE
	
```

- GROUP BY 里的HAVING子句

  

##### ORDER BY

> 当使用select语句查询表中的数据时，结果会按照表数据默认位置进行排序

```mysql
SELECT column1,column2,...
	from table_name
order by field_name [asc|desc]    -- 后面的列是在前一列排好的基础上排序的
select * from goods order by field(field_name,'value','value','value') desc;    -- 自定义排序规则
```

### 关联查询  

#####  表与表之间有关系，通过关系去查询

MySQL支持以下类型的连接

交叉连接

```mysql
selct 
	t1.id,t2.id
from t1
cross join t2
```

内连接、左连接、右连接

```mysql
-- inner join查询示例
select cname,gname from category inner join goods on goods.cid=category.id;
-- left join查询示例
select cname,gname from category left join goods on goods.cid=category.id;
-- right join查询示例
select cname,gname from category right join goods on goods.cid=category.id;
```

### 联合查询

```mysql
SELECT filed from table_name
union all
UNION select gname from table_name
```

### 子查询

> 子查询允许把一个查询嵌套在另一个查询中

##### 子查询分类

###### 标量子查询

```mysql
SELECT * FROM artical where uid=(SELECT UID FROM user WHERE status=1 ORDER BY uid DESC LIMIT 1)
select * from goods where cid = (select id from category where cname='食品');
select * from goods where cid in (select id from category where cname='食品' || cname='饮品');
```

###### 列子查询

###### 行子查询

###### 表子查询

### 聚合函数

- avg()函数         求一组值的平均值
- count()函数     
- instr()函数
- sum()函数
- min()函数
- max()函数
- group_concat()函数     将查询函数的结果连接起来

##### 字符函数

###### CONCAT()函数

> 要连接两个或多个引用的字符串值，请将字符串放在一起

```mysql
select concat('firstname','lastname')
from customers
```

###### LEFT函数

> 函数是一个字符串函数，它返回从左至右指定长度的字符串

```mysql
select LEFT('wasd',2);
```

###### REPLACE()函数

> 它允许你用新的字符串替换表中列的字符串

```mysql
UPDATE tb1 SET f1=REPLACE(f1, 'abc', 'def'); 
REPLACE(str,from_str,to_str)
eg:  SELECT REPLACE('www.mysql.com', 'com', 'cn'); 
```

###### SUBSTRING()函数

> 从特定位置开始的字符串返回一个给定长度的子字符串

```mysql
SUBSTRING(string,position);
SUBSTRING(string,position,length);
```

###### TRIM()函数

> 删除不必要的前导和尾随字符

```mysql
trim([{BOTH|LEADING|TRAILING}]) [remove_str]
```

###### FORMAT()函数

```mysql
FORMAT(N,D,locate);
-- N 是要格式化的数字
-- D 要保留的小数位
-- locate 是一个可选参数，用于确定千个分隔符和分隔符之间的分组
```

##### 日期和时间函数

###### 返回当前日期函数

```mysql
select curdate()         -- 当前日期
select now()             -- 当前日期时间
select sysdate()         -- 程序执行的时间
```

###### 返回指定日期函数

```mysql
select day(now());      -- 返回当前是几号
select month(now());      -- 返回当前的月份
select year(now());      -- 返回当前的年份
select week(now());      -- 返回当前是第几周
select weekday(now());      -- 返回当前是星期几（0 星期日，1 星期一 ....）
select dayname(now());      -- 返回当前是星期几（0 星期日，1 星期一 ....）
set @@lc_time_names = 'zh_CN'；   -- 默认为en_US
```

##### 日期计算函数

###### DATEDIFF（）

```mysql
SELECT DATEDIFF('2018-12-03','2018-12-05');
```

###### TIMEDIFF（）

```mysql
SELECT TIMEDIFF('2018-12-03 12:00:00','2018-12-03 14:00:00');
```

###### TIMESTAMPDIFF()

```mysql
-- 计算两个DATE或DATETIME之间的间隔
TIMESTAMPDIFF(unit,begin,end)
-- unit参数可为：MICROSECOND,SECOND,MINUTE,HOUR,DAY,WEEK,MONTH,QUARTER,YEAR
```

###### DATE_ADD（）

```mysql
DATE_ADD(start_date,INTERVAL,expr unit)
-- INTERVAL是要添加的到起始日期的间隔值
-- expr被视为一个字符串，符合日期格式的字符串
```

### 视图

> 在mysql里面，经常会有一些复杂的查询，对于复杂的查询，每一次查询都是对于性能的消耗。通俗的讲，视图就是一条SELECT语句执行后返回的结果集 。

##### 创建视图

```mysql
create view viewname as select ...
```

##### 修改视图

```mysql
alter view viewname as select ...
```

##### 使用create or replace view语句修改视图

```mysql
create or replace view viewname as select ...
```

##### 删除视图

```mysql
drop view [databases.name].[viewname]
```

### 临时表

##### 创建mysql临时表

```mysql
-- 要创建临时表，只需要将TEMPORARY关键字添加到CREATE TABLE语句中间
CREATE TEMPORARY TABLE select ...
```

##### 删除临时表

```mysql

```

## TCL（Transaction Control Language）事务控制语言

### 事务

> 事务是数据库处理操作，其中执行就好像它是一个单一的一组有序的工作单元，换言之在组内每个单独的操作是成功的，那么一个事务才是完整的。如果事务中的任何操作失败，整个事务将失败。

##### 事务性

- 原子性：确保了工作单位中的所有操作都成功完成，否则，事务被终止，在失败时会被回滚到事务操作以前的状态
- 一致性：事务要求所有的DML语句操作的时候，必须保证同时成功或者同时失败 
- 隔离性：使事务相互独立的操作，事务A和事务B之间具有隔离性 
- 持久性：确保了提交事务的结果或系统故障情况下仍然存在作用

##### 事务控制语句

- BEGIN或START TRANSACTION ；显式的开启一个事务
- COMMIT；也可以使用COMMIT WORK，不过二者是等价的，COMMIT会提交事务，并使已对数据库的修改成为永久的
- ROLLBACK; 可以使用ROLLBACK WORK，不过二者是等价的，回滚会结束用户的事务，并撤销正在进行的所有未提交的修改
- SET AUTOCOMMIT=0  禁止自动提交
- SET AUTOCOMMIT=1  开启自动提交

### MySQL锁概述

表级锁：开销小，加锁快，不会出现死锁；锁定粒度大，发生锁冲突的概率最高，并发度最低

行级锁：开销大，加锁慢，会出现死锁；锁定粒度最小，发生锁冲突的概率最低，并发度也最高

#### 表级锁

> MySQL的表级锁有两种模式：表共享读锁 和 表独占写锁
>
> 表级锁的存储引擎
>
> - MyISAM引擎
> - MEMORY引擎

##### 表级锁的特点

- 作用范围在表的级别
- 如果加了读锁，对MyISAM表的读操作，不会阻塞其他用户对同一表的读请求，但会阻塞对同一表的写请求
- 如果加了读锁，可以查询锁定表中的纪录，但更新或访问其他表都会提示错误
- 如果加了写锁，对MyISAM表的写操作，则会阻塞其他用户对同一表的读和写操作
- 如果加了写锁，可以读写表中的纪录，但更新或访问其他表都提示错误

##### 如何加表锁

###### 加锁

```mysql
lock table table_name read [local],lock tables table_name write [local];
```

###### 多表加锁

```mysql
lock tabel table_name read [local],lock tables table_name [table_name] write [local];
```

###### 释放锁

```mysql
unlock tables;
```

##### 查询表级锁争用情况

```mysql
show status like 'table%';
-- 或者
show status like '%table';
-- 或者
show processlist;          # 查看当前那些命令在等待，以进行优化
-- 或者
show open tables;          # 当前被锁住的表以及被锁的次数
```

##### 并发插入

> MyISAM存储引擎有一个系统变量concurrent_insert 专门用以控制其并发插入行为，其值分别为0，1，或2

- 当concurrent_insert设置为0时，不容许并发插入
- 当concurrent_insert设置为1时，如果MyISAM表中没有空洞，MyISAM允许在一个进程读表的同时，另一个进程从表尾插入纪录
- 当concurrent_insert设置为2时，无论MyISAM表中有没有空洞，都允许在表尾插入纪录

```mysql
show global variable like 'concurrent_insert';
set global concurrent_insert=2;
```

##### 读写锁优先级

###### 设置写锁的最多次数

```mysql
set global max_write_lock_count=1;
-- 有了这样的设置，当系统处理一个写操作后，就会暂停写操作，给读操作执行机会
```

###### 降低写操作的优先级，给读操作更高的优先级

```mysql
low_priority_updates=1;
sql_low_priority_updates=1;
```

##### 设置写内存

```mysql
max_allowed_packet=1M   # 限制接受的数据报大小,大的插入和更新会被限制掉，导致失败
net_buffer_length=2k  # insert语句缓存值 2k-16M
bulk_insert_buffer_size=8M   #一次性insert语句插入的大小
```

##### 如何优化

```mysql
可以利用MyISAM存储引擎的并发插入特性，来解决应用中对同一表查询和插入的锁争用，例如将concurrent_insert系统变量设置为2,允许在表尾插入纪录
```

#### 行级锁

> MySQL的行级锁有两种模式
>
> 共享锁（S）允许一个事务去读一行，阻止其他事务获得相同数据集的排他锁
>
> 排他锁（X）允许获得排他锁的事务更新数据，阻止其他事务取得相同数据集的共享锁和排他写锁
>
> 意向共享锁（IS）事务打算给数据行加共享锁，事务在给一个数据行加共享锁前必须先取得该表的IS锁
>
> 意向排他锁（IX）事务打算给数据行加排他锁，事务在给一个数据行加排他锁前必须先取得该表的IX锁

| 请求锁模式是否兼容当前锁模式 | X    | IX   | S    | IS   |
| ---------------------------- | ---- | ---- | ---- | ---- |
| X                            | 冲突 | 冲突 | 冲突 | 冲突 |
| IX                           | 冲突 | 兼容 | 冲突 | 兼容 |
| S                            | 冲突 | 冲突 | 兼容 | 兼容 |
| IS                           | 冲突 | 兼容 | 兼容 | 兼容 |

行级锁存储引擎  --  InnoDB

##### 行级锁的特点

- InnoDB行锁是通过给索引上的索引项加锁来实现的，只有通过索引条件检索数据，InnoDB才使用行级锁，否则InnoDB将使用表级锁
- 意向锁是InnoDB自动加的，不需要用户干预。对于update delete insert语句，InnoDB会加排他锁
- 在研究行锁的时候，需要将自动提交关闭，默认为开启

```mysql
set autocommit = 0;   # 多个用户时都要设置该语句
```

##### 如何加行锁

> 给MySQL表显示加锁，一般是为了在一定程度模拟

###### 加锁

```mysql
共享锁： select * from table_name where ... lock in share mode;
排他锁： select * from table_name where .. fro update;
```

###### 释放锁

```mysql
commit;
rollback;
```

##### 注意事项

> ###### InnoDB默认的隔离方式

- 当给一条数据上了排他锁之后，其他用户将无法对该条数据进行操作
- 当访问某行数据时，update、insert或delete语句使得数据被加上排他锁，但这并不影响其他用户访问此表中的别条数据
- 如果说正在操作的字段不是索引类型，那么行锁会自动升级为表锁
- 字段加索引后就可以使用行锁了
- 即使字段加了索引，但当字段类型被改变时，此索引将失效
- 间隙锁，当表中有空洞时，操作包含有间隙的数据时会锁住整张表
- 指定精确的范围，防止锁住其他无辜的数据项

###### 查看行锁的争用情况

```mysql
show status like 'innodb_row_lock%';
```

#### 事务并发问题

1. 脏读：事务A读取了事务B更新的数据，然后B回滚操作，那么A读取到的数据是脏数据
2. 不可重复读：事务A多次读取同一数据，事务B在事务A多次读取的过程中，对数据作了更新提交，导致事务A在多次读取同一数据时出现不一致
3. 幻读：系统管理员A将数据库中所有学生的成绩从具体分数改为ABCDE等级，但是系统管理员B就在这个时候插入了一条具体分数的记录，当系统管理员A改结束后发现还有一条记录没有改过来，就好像发生了幻觉一样，这就叫幻读。

#### MySQL事务隔离级别

##### 各个隔离级别的情况

```mysql
select @@session.tx_isolation;    -- 查看隔离级别
set sesssion transaction isolation level read uncommitted;       -- 设置隔离级别，读未提交
```

##### 读未提交

```mysql

```

##### 读已提交

```mysql

```

##### 可重复读

```mysql

```

MVCC:   多版本并发控制 (Multiversion Currency  Control)

##### 如何优化行级锁

- 尽量使用较低的隔离级别，精心设计索引，并尽量使用索引访问数据，使加锁更精确，从而减少锁冲突的机会
- 选择合理的事务大小，小事务发生锁冲突的几率也更小
- 给纪录集显示加锁时，最好一次性请求足够级别的锁，比如要修改数据的话，最好直接申请排他锁，而不是先申请共享锁，修改时再请求排他锁，这样容易产生死锁
- 尽量用相等条件访问数据，这样可以避免间隙锁对并发插入的影响
- 对于一些特定的事务，可以使用表锁来提高处理速度或减少死锁的概率

## 主从复制

> 在实际的生产环境中，由单台MySQL数据库是完全不能满足实际需求，无论安全性、高可用性以及高并发性等各个方面的要求。

### 主从复制配置过程

#### 基本要求

- 两台服务器
- 两台mysql版本一致，不一致的话主服务器要低于从服务器
- 两台服务器防火墙关闭
- 双方数据库的用户，具有远程访问的权限

### 主服务器配置

修改主服务器的MySQL配置文件

```mysql
# mysql唯一id
server-id = 1
# 二进制日志文件，此项为必填项，否则不能同步数据
log-bin = "mysql-bin"
# 指定二进制错误文件
log-error = "mysql-error"
# 需要同步的数据库，如果需要同步多个数据库
binlog-do-db = demo_shujuku
# bin-do-db = slaveDB1
# bin-do-db = slaveDB2
# 不需要同步的数据库
binlog-ignore-db = mysql
```

授权给从数据库服务器

```mysql
grant replication slave on *.* to 'root'@'192.168.56.1' identified by '154303';
flush privileges;
```

重启服务器

```mysql
service mysqld restart;
/etc/inint.d/mysql restart
sudo /etc/init.d/mysql restart;
```

查看主服务器二进制日志信息

```mysql
show master status;
```

### 从服务器配置

修改从服务器的MySQL配置文件

```mysql
# /etc/mysql/my.cnf     linux里面mysql配置文件目录
server-id = 2
log-bin = "mysql-bin"
replicate-do-db = demo_shujuku
replicate-ignore-db = mysql
read-only       # 设只读权限
sudo chmod 664 /etc/mysql/my.cnf
```

重启MySQL服务

执行同步sql语句

```mysql
change master to
master_host = '192.168.119.131',
master_user = 'root',
master_password = '154303',
master_log_file = 'mysql-bin.000002',
master_log_pos = 107;
```

启动Slave同步进程

```mysql
stop slave;
start slave;
```

主从同步检查

```mysql
show slave status\G
```

#### 二进制日志

查看二进制日志

```mysql
show binary logs;      # 二进制文件
show master logs;
```

##### 删除某个二进制

```mysql
purge binary logs to xxx;
```

##### 清除所有的二进制日志文件

```mysql
reset master;
```

##### 自动清理

```mysql
show variables like 'expire_logs_days';
set expire_logs_days=7;
```

## MySQL数据库优化操作

> 数据库优化维度有四个：硬件、系统配置、数据库表结构、SQL及索引

### explain参数详解

> 查看一个这些sql语句的执行计划和查询效率，该命令从sql执行的执行顺序

#### id

> id是sql执行顺序的标识



#### select_type

> 查询中每个select子句的类型
>
> /usr/local/nginx/sbin



#### table

> 显示这一行的数据是关于哪张表的，看到的是derivedx的，说明这个结果是派生表的结果

#### type

> 表示MySQL在表中找到所需行的方式，又称“访问类型”，代表性能的优劣，常用类型有ALL<index<range<ref<eq_ref<const<system<NULL

- ALL: Full table Scan,  MySQL将遍历全表以找到比配的行，并且查找的内容不带索引
- index: Full Index Scan,  index与ALL区别为index类型只遍历索引树，也就是查找有索引的树
- range: 只检索给定范围的行，查找内容不带索引，选择的行带索引，可以用between,>,<，但是不要用in，用in索引失效
- ref: 表示上述表的连接匹配条件，即那些列或常量被用于查找索引列上的值，使用普通索引
- eq_ref: 类似ref，区别就在使用的索引是唯一，对于每个索引键值，表中只有一条纪录匹配。就是多表连接中使用primary key 或者 unique key 作为关联条件
- const、system: 当MySQL对查询某部分进行优化，并转换为一个常量时，使用这些类型访问，如将主键置于where列表中，MySQL就能将该查询转换为一个常量
- system

#### possible_keys

> 

#### key

> 

#### key_len

> 

#### ref

> 

#### Extra

> 该列包含MySQL解决查询的详细信息，

Using filesort:  MySQL进行了多次排序，没有利用索引进行排序，说明性能很低

### MySQL优化方法

#### 优化工具

- 通过使用explain命令分析sql语句的运行效率
- 通过开启慢查询来查看运行效率慢的sql语句

#### 索引优化

> 索引是我们提升sql查询效率的重要手段，同时索引是使用不当也会带来性能低下

1.不能将索引用作表达式的一部分，也不能是函数的参数

```mysql
select * from demo where id+1=2
select max(id) from demo where id=1;
```

2.索引不要进行类型转化，否则索引失效

```mysql
select * from demo where name=2
# 如果name是字符串类型，就存在类型转换
```

3.复合索引应该遵循左前缀策略，不要交叉使用

```mysql
alter table table_name add index a_b_c(a,b,c)
select c from table_name where id=a order by b
```

4.符合索引如何用“or”关键字,索引失效

```mysql
select * from table_name where a='' or b=''
```

5.符合索引不要用 !=  <>  或 is null (is not null)

6.尽量不要和in,可以使用between

```mysql

```

7.及时删除不用的索引

8.like查询时尽量左边不要出现%

```mysql

```

#### 表级别锁优化

#### 系统优化

1. 主从复制
2. 读写分离
3. 负载均衡

#### 其他优化总结

1. 通常来说可以把NULL的列改为NOT NULL不会对性能提升有多少帮助，只是如果计划在列上创建索引，就应该将该列设置为NOT NULL
2. 对于数据类型，一定要根据业务需求选择尽可能小的存储数据类型
3. UNSIGNED表示不允许负值，大致可以使正数的上限提高一倍


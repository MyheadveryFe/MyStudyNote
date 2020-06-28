# 数据库基础知识

关系型: MySQL, Oracle, SqlServer SQLlite

非关系: Redis, MongoDB

DBMS 数据库管理系统



# MySQL基础知识

连接: mysql -u root -p

修改用户密码:  

```mysql
update mysql.user set authentication_string=password('123456') where user='root' and Host ='localhost'; //mysql8.0以上不适用
```

刷新权限:

```mysql
flush privileges;
```

show databases;

use mysql;

show tables;

describe 表名; //显示表的具体信息

create database 名;

单行注释 --

多行注释 /**/

drop database '名';//删除数据库



# 数据库语言

DDL 定义语言

DML 操作语言

DQL 查询语言

DCL 控制语言



# 操作数据库

创建 : create database if not exists 名;

查看创建数据库的语句: show create database 数据库名; 

删除: drop database if exists 名;

使用 use 名;

查看所有 show databases;

## 数据库数据类型

tinyint 1字节;

smallint 2字节

int 4

mediumint 3

bigint 8

float 4

double 8

decimal 字符串形式浮点数 计算金额



char  字符串  0-255

**varchar  可变字符串  0-65535  对应String**

tinytext  微型文本  2^8-1

**text  文本串  保存大文本**

date  YYYY-MM-DD

time  HH:mm:ss 

**datetime   最常用的时间**

**timestamp  时间戳**

year 年份



## 数据库字段属性

unsigned 无符号整数

zerofill 零填充, 不足位用0填充

自增auto_increment, 非空not null, 默认default

## 每一个项目必须有的键

id 主键, 'version' 乐观锁, is_delete 伪删除, gmt_create 创建时间, gmt_update 修改时间



## 数据库表的基本知识

显示表结构 desc 表名;

### 数据库引擎

InnoDB 默认使用

MYISAM

区别: InnoDB不支持全文索引, 表空间占用大, 安全性高, 支持事务/行锁/外键, 多表多用户操作

MYISAM: 速度快, 节约空间, 支持全文索引, 占用空间小

**数据库文件存放**: mysql/data目录下



# 创建表

格式:

```mysql
create table if not exists `表名` (
	`字段名` 列类型 属性 索引 注释,
    `id` int(4) not null auto_increment comment '学号',
    `name` varchar(20) not null default '匿名' comment '姓名',
	`字段名` 列类型 属性 索引 注释,
	...
	`字段名` 列类型 属性 索引 注释
	primary key(`名`),
	其他索引
)engine=innodb default charset=utf8 注释
```

**注意**: 表名列名可以用键盘左上角的那个点 ` 包裹, 注释或者字符串用单引号 ' 包裹

# 修改表

修改表名: alter table 表名 rename as 新表名;

增加表字段: alter table 表名 add 列名 列类型 属性 索引 注释

修改字段: alter table 表名 modify 列名 列类型 ...;   //修改的是列属性, 全部属性都要填上否则为空

​				alter table 表名 change 原表名  新表名 列类型..; 修改表名, 全部属性都要带上

删除表字段: alter table 表名 drop 列名;

删除表: drop table if exists 表名



# 外键

## 创建外键

方式1: 创建表时增加外键

key \`FK_gradid\` (\`gradeid\`),   //这句是增加普通索引

constraint \`FK_gradeid\` foreign key (\`gradeid\`) references \`grade\`(\`gradeid\`)   //这句是增加外键

方式2: 已有表创建外键

alter table 表名 add constraint 外键名 foreign key (列名) references 表名(列名);

## 删除外键

alter table 表名 drop constraint 外键名;

alter table 表名 drop foreign key 外键名;

### 删除带外键的数据

SET FOREIGN_KEY_CHECKS=0;

删除，更新数据，

恢复外键

SET FOREIGN_KEY_CHECKS=1;

另：查看当前 FOREIGN_KEY_CHECKS的值

SELECT @@FOREIGN_KEY_CHECKS;



# DML语言

数据库操作语言

## 添加insert

**添加一行记录**

insert into 表名 ([字段名1，字段2，字段3]) values('值1'),('值2'),('值3'),....

insert into 表名 (字段1,字段2, ...)  values(值1, 值2,...);

## 修改update

**修改某行的某列数据**

update 表名 set 列名 = 值, 下一个列名 = 值  where 条件;

条件: = <> != between...and..., and, or

无指定则修改所有

## 删除delete

**删除某行或某些行**

delete from 表名 where 条件

truncate table 表名  //完全清空一个表, 属性和索引不变

truncate会重新设置自增列, 不影响事务

**innodb自增列持久化问题**

innodb自增主键没有持久化到硬盘中, 是在内存中维护一个字典, 重启innodb后会从最大的那个id开始计算, 

在MySQL 8.0中引入自增列持久化特性，可以避免上述问题

myisqm是存在文件中不会丢失

# DQL查询语言

> select语法

select 字段 from 表 

select 字段 as 别名 from 表 as 别名

使用别名加as 或不加 都是一样的

去重查询:

select **distinct** 字段 from 表

查询计算结果

select 100*3 as 别名

查询自增步长

select @@ auto_increment_increment

数据加一

select 字段+1 as 别名 from 表



where:

模糊查询:

like %代表0到任意个字符, _代表一个字符

where 字段 like '刘%';

in (具体的一个或多个值) //不能用%和_

where 字段 in (值, 值, 值,...);

null      not null

where 字段='' or 字段 is null;



## 连表查询

join on

### left join, inner join, right join

select s.字段, 字段, 字段, 字段 from 表名 别名 left join 另一个表名 别名 on 别名.字段 = 别名.字段;

左连接: 从select后面的字段名组成新表的字段, 左连接条件中, 别名1.字段1 = 别名2.字段2, 如果左边有某些行无法在右边找到匹配的, 则将该行也加入到新表中, 新表中属于右表的字段则显示为空

内连接: 只有完全匹配的行才会显示在新表中

右连接: 右表不能匹配上左边的行也要加入到新表中, 新表中属于左表的字段则显示为空

 自连接: select 字段, 字段 from 表 as 别名1, 同一表 as 别名2 where 别名1.字段=别名2字段;



### 分页limit, 排序order by

ASC升序, DESC降序

order by 字段 asc;

limit 起始位置, 页面大小

## 子查询

select 字段 from 表 别名 where 别名.字段=( 新的select语句);

## group by , having

要与聚合函数配合使用

group by 按字段分组, 可配合count使用

having再配合group by 使用

having 条件, 本质和where相同, 都是筛选



# MySQL函数

## 数学运算

abs() 绝对值

ceiling() 向上取整

floor() 向下取整

rand() 0-1随机数

sign() 判断一个数的符号, 负数返回-1

char_length() 返回字符串长度

concat() 字符串拼接

insert() 插入替换

lower(), upper()

instr() 返回第一次出现的字符串的位置

replace() 替换出现的指定字符串

substr()

reverse() 反转

## 时间函数

current_date()  获取当前日期

curdate()

now() 获取当前时间

localtime()

sysdate()

## 系统

user()

system_user()

version()

## 聚合函数（常用）

count avg sum max min

count(字段)  忽略null计算行数

count(*) 或count(1) 不忽略null计算所有行数

## MD5加密

MD5(pwd)



# 事务

事务原则: ACID 原子性, 一致性, 隔离性, 持久性

MySQL默认开启事务

开启: set autocommit = 1/0关闭

创建事务流程

```mysql
set autocommit = 0;
start transaction;
xx
commit/rollback;
set autocommit = 1;

savepoint 保存点名  --设置保存点
rollback to savepoint 保存点名  --回滚到保存点

```



# 索引

加快搜索速度, 保证字段唯一性

主键索引 primary key(字段)

唯一索引 unique key(字段)

```mysql
alter table student add constraint unique_name unique index(`name`) using btree;
alter table 表名 add unique key 索引名(字段名);
```

常规索引 key/index 名 字段

```mysql
index 索引名(字段) using btree;  --用key也可以
```

全文索引 fulltext

只有MYISAM才有

**显示所有索引**: show index from 表名

增加索引: 

```mysql
alter table 表名 add fulltext index 索引名(字段名);
```

explain查看sql执行状况

explain select * from student;

## 索引原则

非越多越好

经常变的不要加索引

小数据量的表不加

常用查询的字段要加

**索引默认数据结构** btree



# 权限管理

## 待续

用户权限



# 数据库备份

使用cmd导出

mysqldump -hlocalhost -uroot -p密码 数据库名 表名 > 物理磁盘位置/文件名

导入: cmd登入mysql, source 绝对地址



# 三大范式

第一范式: 每一列不可分割的原子数据项

第二范式: 满足第一范式, 每张表只描述一件事

第三范式: 满足第二范式, 每一列数据都与主键直接相关, 不能间接相关

## 范式与性能问题

性能更重要

关联查询不超三张表

可额外加一些计算列

故意冗余从而多表查询变单表查询










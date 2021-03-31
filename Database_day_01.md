## 学习网址 ##
[https://www.runoob.com/mysql/mysql-tutorial.html](https://www.runoob.com/mysql/mysql-tutorial.html)
## 常用命令 ##
### 启动及关闭mysql ###
1. 启动mysql服务：`net start mysql`
2. 登录mysql，需要进入mysql安装目录：`mysql -u root -p`
3. 查看mysql命令：`help;`
4. 推出mysql：`exit;`
5. 关闭数据库服务：`net stop mysql`
### 管理mysql的命令 ###
1. 列出数据库管理系统的数据库列表：`show databases;`
2. 进入数据库：`use database_name;`
3. 显示数据库中的所有表：`show tables;`
4. 显示表的属性，属性类型，主键信息：`show columns from table_name;`
### 创建与删除 ###
- 创建数据库：`create database database_name;`
- 删除数据库：`drop database database_name;`
- 使用数据库：`use database_name;`

- 创建数据表：`create table table_name (column_name column_type);`
	实例解析： 
	`create table if not exist 'runoob_tb1' (
		'id' int unsigned auto_increment,
		'title' varchar(100) not null,
		'author' varchar(40) not null,
		'date' date,
		primary key('id')
	)engine=innodb default charset=utf8;`
	auto_increment定义列为自增的属性，一般用于主键，数值会自动加1
	primary key用于定义列为主键，可以用多列来定义主键，列间用括号分隔
	engine设置存储引擎，charset用来设置字符集。
	上面表名和字段名不是单引号，而是~。
	
- 删除数据表：`drop table table_name;`
## Mysql数据类型 ##
link:[https://www.runoob.com/mysql/mysql-data-types.html](https://www.runoob.com/mysql/mysql-data-types.html)
Mysql支持多种类型，大致可以分为三类：数值，时间和字符串
### 数值类型 ###
|  类型  |  大小  |  范围  |  用途  |
| ----   |----   |  ----- | ----- |
|int     | 4bytes| (-2147483648,2147483647)|大整数值|
|bigint|8bytes|(-9223372036854775808,)|极大整数|
|float|4bytes|()    |单精度浮点数|
|double|8bytes|()|双精度浮点数|
### 时间和日期类型 ###
|类型|大小|格式|用途|
| ----   |----   |  ----- | ----- |
|date|3|YYYY-MM-DD|日期|
|time|3|HH:MM:SS|时间|
|datetime|8|YYYY-MM-DD HH:MM:SS|日期与时间|
|timestamp|4|YYYYMMDD HHMMSS|时间戳|
### 字符串类型 ###
|类型|大小|用途|
| ----   |----   |  ----- |
|char|0-255bytes|定长字符串|
|varchar|0-65536bytes|变长字符串|
|text|0-65536bytes|长文本数据|
|longtext|0-4294967295bytes|极大文本数据|
## 数据表的增删改查
### 插入
- 语法：`insert into table_name(filed1, filed2) values (value1, value2);`
### 查询
- 语法：`select column_name1, column_name2 from table_name [where clause] [limit n] [offset m];`
- where包含查询条件，limit设定返回的记录数，offset指定查询的数据偏移量，默认为0
#### where子句
- 语法：`select filed1, filed2 from tb1, tb2 [where condition1 [and | or] condition2];`
- where子句的字符串比较不区分大小写，可以使用binary来区分大小写
### 更新
- 语法：`update table_name set filed1=newval, filed2=newval [where condi];`
- 用于修改表中的记录
### 删除
- 语法：`delete from table_name [where condi];`
- 用于删除表中的记录
### 模糊查询
- 语法：`select filed1 from table_name where file1 like condi;`
- like通常与%一起使用，%表示任意字符


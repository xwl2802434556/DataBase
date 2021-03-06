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
- 用于：修改表中的记录
### 删除
- 语法：`delete from table_name [where condi];`
- 用途：用于删除表中的记录
### 模糊查询
- 语法：`select filed1 from table_name where file1 like condi;`
- 用途：用来模糊查询。like通常与%一起使用，%表示任意字符

### Union ###
- 语法：
	`select field1 from table1 [where condi]
	 union [all | distinct]
	 select field1 from table2 [where condi]
	`
- 用途：用于连接两个以上的select语句结果到一个结果(一列)中，重复的数据会被删除。
### 排序Order by ###
- 语法：
	`select filed1 from table1 
	 order by filed1 [asc | desc], filed2 [asc | desc]`
- 用途：对需要读取的数据进行排序
### 分组Group by ###
- 语法：
	`select field1, fun(field2) from table1
	 [where condi] group by field1;`
- 用途：用于统计一列或多列的性质，通常与函数count, sum, avg使用，比如统计name这一列中姓名出现的次数
- 例子：select name, count(*) from employee_tb1 group by name;
### 连接JOIN ###
- 语法：
	`select a.id, b.name 
	 from tbl1 a join tbl2 b on a.id = b.id;`
- 用于：用于查询多张表中的数据
	- [inner ]join(内连接，等值连接):获取两张表中字段匹配关系的记录
	- left join(左连接):获取左表中所有记录，即使右表中没有对应的记录
	- right join(右连接)
- 例子：
	`select a.runoob_id, a.runoob_author, b.runoob_count 
	from runoob_tbl a join tcount_tbl b on a.runoob_author = b.runoob_author;
	select a.runoob_id, a.runoob_author, b.runoob_count 
	from runoob_tbl a,  tcount_tbl b where a.runoob_author = b.runoob_author;`
### 导入导出.sql文件 ###
- 导入：source a.sql
- 导出：mysqldump -u 用户名 -p 数据库名 > 存放位置
### NULL值处理 ###
- is null运算符：当列的值为null，返回true
- is not null：当列的值不为null，返回true
- ifnull(col1, 0):col1类型为int，如果col1为null，则返回0
### Mysql正则表达式 ###
- 语法：`select col1 from tb1 where col regexp '^123$'`
### Mysql事务 ###
- 事务满足四个条件：原子性，一致性，隔离性，持久性。
- 使用：`begin; sql; commit;` `begin; sql; rollback;`
### ALTER命令 ###
- 用途：修改数据表名，字段名
- 例子：
	- create table testalter_tbl(i int, c char(1));
	- show columns from testalter_tbl;
	- alter table testalter_tbl drop i; 删除表中的i字段
	- alter table testalter_tbl add i int;增加i字段，并定义数据类型,默认放在最后一列
	- alter table testalter_tbl add a int first;
	- alter table testalter_tbl add a int after c;
	- alter table testalter_tbl modify c char(10);修改字段类型
	- alter table testalter_tbl alter i set default 100;设置默认值
	- alter table testalter_tbl alter i drop default;删除默认值
	- ALTER TABLE testalter_tbl ENGINE = MYISAM;修改引擎
	- SHOW TABLE STATUS LIKE 'testalter_tbl'\G;
	- ALTER TABLE testalter_tbl RENAME TO alter_tbl;
+++

title = "SQL语句"
date = 2017-03-01T00:00:00+08:00
categories = ["读书笔记"]
toc = true
author = "ElvisSong"
author_homepage =  "https://elvissong.github.io/post/"
+++

### SQL DML 和 DDL
可以把 SQL 分为两个部分：数据操作语言 (DML) 和 数据定义语言 (DDL)。
SQL (结构化查询语言)是用于执行查询的语法。但是 SQL 语言也包含用于更新、插入和删除记录的语法。

查询和更新指令构成了 SQL 的 DML 部分：

* SELECT - 从数据库表中获取数据
* UPDATE - 更新数据库表中的数据
* DELETE - 从数据库表中删除数据
* INSERT INTO - 向数据库表中插入数据

SQL 的数据定义语言 (DDL) 部分使我们有能力创建或删除表格。我们也可以定义索引（键），规定表之间的链接，以及施加表间的约束。

SQL 中最重要的 DDL 语句:

* CREATE DATABASE - 创建新数据库
* ALTER DATABASE - 修改数据库
* CREATE TABLE - 创建新表
* ALTER TABLE - 变更（改变）数据库表
* DROP TABLE - 删除表
* CREATE INDEX - 创建索引（搜索键）
* DROP INDEX - 删除索引

select * from 表名 或者 select 列名 from 表名

关键词 distinct 用于返回唯一不同的值

select distinct 列名 from 表名 

select 列名 from 表名 where 列 运算符 值

运算符 | 描述
-- | --|
= | 等于 |
<> | 不等于
> | 大于
< | 小于
>= | 大于等于
<= | 小于等于
between | 在某个范围内
like | 搜索某种模式

and 和 or  且与或

select * from Persons where Lastname='peter'


top 子句用于规定要返回记录的数目

select top number | percent column_name(s) from table_name

select top 50 percent * from Persons

like 用于在 where 子句中搜索列中的指定模式

select column_name(s) from table_name where column_name like pattern

select * from Persons where City like 'N%' 选取Persons表中居住地以N开头的城市的人；

### SQL 通配符
通配符 | 描述
-- | --
% | 替代一个或多个字母
_ | 仅替代一个字母
[charlist] | 字符列中的任何单一字符
[^charlist] 或者 [!charlist] | 不再字符列中的任何单一字符

IN 操作符允许我们在 where 子句中规定多个值

select column_name(s) from table_name where column_name IN (value1, value2,...)

Between 在where子句中使用，选取介于两个值之间的数据范围

select column_name(s) from table_name where column_name Between value1 and value2

alias 给表名一个别名

select column_name(s) from table_name as alias_name

SELECT po.OrderID, p.LastName, p.FirstName
FROM Persons AS p, Product_Orders AS po
WHERE p.LastName='Adams' AND p.FirstName='John'


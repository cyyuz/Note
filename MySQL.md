```mysql
mysql -uroot -p123456          // 登录
exit                           // 退出
show databases;                // 查看mysql中有哪些数据库
use test;                      // 选择使用某个数据库
create database bjpowernode;   // 创建数据库
show tables;                   // 查看某个数据库下有哪些表


select version();              // 查看mysql数据库的版本号
select database();             // 查看当前使用的是哪个数据库
```
<table>
	<tr>
		<th>分类</th>
		<th>描述</th>
		<th>命令</th>
	<tr/>
	<tr>
		<td>DQL</td>
		<td>数据查询语言</td>
		<td>select查</td>
	</tr>
	<tr>
		<td>DML</td>
		<td>数据操作语言</td>
		<td>insert增、delete删、update改</td>
	</tr>
		<tr>
		<td>DDL</td>
		<td>数据定义语言</td>
		<td>create新建、drop删除、alter修改</td>
	</tr>
	<tr>
		<td>TCL</td>
		<td>事务控制语言</td>
		<td>事务提交commit、事务回滚rollback</td>
	</tr>
	<tr>
		<td>DL</td>
		<td>数据控制语言</td>
		<td>授权grant、撤销权限revoke</td>
	</tr>
</table>




```
DQL： 数据查询语言（带有select关键字的都是查询语句）
     select…
DML： 数据操作语言（对表当中的数据进行增删改）
       insert 增
       delete 删
       update 改
DDL： 数据定义语言（凡是带有create、drop、alter的都是DDL）
     DDL主要操作的是表的结构。不是表中的数据。
     create：新建，等同于增
     drop：删除
     alter：修改
     这个增删改和DML不同，这个主要是对表结构进行操作。
TCL： 事务控制语言，包括：
    事务提交：commit;
    事务回滚：rollback;
DCL： 数据控制语言
    例如：授权grant、撤销权限revoke…
```

## DQL
```
select                       
		...	
from
		...
where
		...
group by
		...
having
		...
order by
		...
limit
		...
执行顺序？
		1.from
		2.where
		3.group by
		4.having
		5.select
		6.order by
		7.limit..
```

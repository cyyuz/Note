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
		<td>	DQL	   				</td>
		<td>	数据查询语言				</td>
		<td>	select查		</td>
	</tr>
	<tr>
		<td>	DML						</td>
		<td>	数据操作语言					</td>
		<td>	insert增、delete删、update改			</td>
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

<table>
	<tr>
		<th>分类</th>
		<tr>
			<th>分类</th>
			<th>描述</th>
			<th>命令</th>
		<tr/>
		<tr>
			<th>分类</th>
			<th>描述</th>
			<th>命令</th>
		<tr/>
	<tr/>
</table>

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

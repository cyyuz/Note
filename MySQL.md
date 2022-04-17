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

```
DQL： 数据查询语言（凡是带有select关键字的都是查询语句）
     select…
DML： 数据操作语言（凡是对表当中的数据进行增删改的都是DML）
     insert 增
     delete 删
     update 改
     这个主要是操作表中的数据data。
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

### mysql引擎

![img](H:\gitwork\notes\VMware\CRUD.assets\20181010091048777.png)

MyISAM引擎现在很少被使用，Mysql默认使用InnoDB;

TokuDB只支持Linux版的mysql，用于很少被查询的归档数据，插入速度与数据压缩等都不InnoDB性能高很多。



* 批量插入一批数据，因为一条记录的问题，全部数据都写入失败

  通过在Insert 后面加 Ignore即可只插入正确的记录，而不会导致所有的插入语句都回滚。

  ![1570252114019](H:\gitwork\notes\VMware\CRUD.assets\1570252114019.png)

  不加Ignore则会报错，40主键已经存在，因此所有的数据都不会被插入

  ![1570252204419](H:\gitwork\notes\VMware\CRUD.assets\1570252204419.png)

  加Ignore，影响的行数只有3行

* 不存在就插入，存在就更新

  ```mysql
  	insert into t_emp_ip (id ,empno,ip)
  	values 
  	(5,8007,"192.168.99.49"),
  	(6,8008,"192.168.99.50"),
  	(7,8009,"192.168.99.51"),
  	(8,8001,"192.168.99.52")
  	on DUPLICATE KEY UPDATE ip=VALUES(ip);
  ```

  

#### 要不要使用子查询

* Mysql数据库默认关闭了缓存，所以每个子查询都会相关子查询

* 相关子查询就是循环执行多次的子查询

  ![1570264113581](H:\gitwork\notes\VMware\CRUD.assets\1570264113581.png)

> 因为Mybatis等持久层框架开启了缓存功能，其中一级缓存就会保存子查询的结果，所以可以放心使用子查询
>
> 结论：SQL控制台不要使用子查询，在持久性框架则可以使用

#### 如何替代子查询？

![1570264343574](H:\gitwork\notes\VMware\CRUD.assets\1570264343574.png)

![1570264397755](H:\gitwork\notes\VMware\CRUD.assets\1570264397755.png)

![1570264448857](H:\gitwork\notes\VMware\CRUD.assets\1570264448857.png)

​			第一个会保留所有t_emp表中的所有数据（t_dept为null），而第二个则没有d.deptno=10的数据



#### 表连接修改

![1570264698406](H:\gitwork\notes\VMware\CRUD.assets\1570264698406.png)

​	第一个sql依然是相关子查询（每过滤一条数据，子查询就会执行一次），

​	第二个sql表连接，可以**同时更改多个表的数据**（nb）

#### 表连接删除

![1570264887475](H:\gitwork\notes\VMware\CRUD.assets\1570264887475.png)








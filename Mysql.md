# Mysql数据库

## Mysql的描述

是一种关联数据库管理系统，体积小，速度快，开源，因此大大降低了总体成本。

## 安装和进入

linux下的安装:

```shell
$ sudo apt install Mysql-server
设置密码为123456
```

密码忘记:

```shell
$ sudo passwd root
需要输入用户密码
```

进入：

```shell
$ mysql -u root -p
```

## 基本使用(语句结尾要注意有分号)

### mysql的基本命令

1. help(\h) --> 帮助
2. \q 或者 quit 或者 exit --> 退出
3. show databases; --> 显示当前数据库
4. use tables; --> 进入某个数据库
5. show tables; --> 显示所有的表
6. desc version(或者表名); --> 查看表机构

### sql语句

#### 概念

SQL是结构化查询语言，用于存取数据以及查询更新和管理关系型数据库系统，sql语句是对数据库进行操作的一种语言

常见概念：表，字段，记录，字段名，字段元素

#### 使用

##### DDL(数据定义)

1. 数据库的创建和删除(数据库名以db结尾)

```sql
/`创建 
(1) create database databasename;  --> 创建数据库默认编码格式为ASCii
(2) create database databasename default character set utf8 collate utf8_general_ci; --> 编码格式为utf8

// 删除
drop database databasename; --> 删除数据库
```

2. 创建一个表

```sql
  //创建
  create table tablename(id int(10) not null auto_increment primary key, name varchar(64) not null,age int, score float default 0.0); --> 创建表
```
注意:表名后面用括号包含字段设置，每个字段直接用逗号隔开，字段名在前，修饰在后，int类型不加参数默认长度为11，最好按照上述顺序写修饰，使用varchar必须写长度，auto_increment是自动增加，一般用在id,primary key 是设置主键，一般把id设置为主键

```sql
drop table tablename; --> 删除表
```

```sql
//改名
alter table oldname rename newname; --> 改表名
```
3. 对字段的操作

```sql
//修改字段类型
alter table stu modify 字段名 字段类型; 
```

```sql
//增加字段，若有after，column后面不加括号包含新字段
 alter table stu add column 字段名，修饰1，修饰2.. after 字段名;
```
```sql
//删除字段
alter table stu drop column 字段名;
```

```sql
//段改名字，可以写可以不写type
alter table stu change oldname newname type;
```

```sql
//默认值
alter table stu alter 字段名 set default 100; --> 修改默认值
 alter table stu alter 字段名 drop default; --> 删除字段默认值
```
##### DML(数据操纵) -记录的增删改查

```sql
//增加
insert into tablename values (,,,)  --> 若是所有字段都要赋值可以这写
insert into tablename (field1,field3) values (value1,value3) --> 指定要赋值的字段
```
```sql
//查询
select * from table --> 查询表中所有字段
select * from table where expression --> 按照条件查询记录的所有字段
select table.id from table where expression
```

```sql
//删除
delete from table where expression --> 删除指定条件的记录
```

```sql
//更新
update tablename set f1=value1,f2=value2 where expression --> 对满足条件的记录的对应字段值进行更改
```

## 常见问题

### 什么是主键？什么是外键？

主键:关系型数据库中的一条记录中有若干个属性，若其中某一个属性组(注意是组)能唯一标识一条记录，该属性组就可以成为一个主键 
外键:内联外联用的，在一个表汇总出现另一个表的主键就叫做外键

### 内连接和外连接有什么不同？左连接，右连接和全连接的区别?

内连接：2个有关系的表完全进行关联，外连接是2个有关系的表进行关联，没有关联的也会出现

```sql
 select teacher.id,teacher.teacher,student.id,student.name  from student,teacher where teacher.stu = student.name;
//注意:前面的顺序决定显示出来的顺序，所谓的内联就是完全满足条件的联系，其他不显示
```
左连接，右连接和全连接都是外连接，

```sql
// mysql中
左联：s left join on t  --> 前面的完全显示s，
右联：t right join on s --> 后面的s完全显示s,和左联等同
```
### 说下mysql的索引

索引：索引是一种单独的、物理的对数据库表中一列或多列的值进行排序的一种存储结构，它是某个表中一列或若干列值的集合和相应的指向表中物理标识这些值的数据页的逻辑指针清单。
优点：根据某一行或几列创建一个索引，可以使我们快速的查找数据
缺点：创建索引占用一部分存储空间，在插入和修改数据时索引也会随之变化，可能需要一定的时间

由引擎决定如何创建，一般采用B树或者B+树的结构

什么情况下需要：需要大大加快数据的检索速度，加速表和表之间的连接，性能的提供

###  事务

只作为单个逻辑工作单元执行的一系列操作，要么完全执行要么不执行

特征：原子性 一致性（开始到结束不会被破坏） 持久性   隔离性

原子性操作：必须完全进行完毕

### 引擎选择

Innodb(默认)：本身提供了事务支持。写操作速度快，在并发较高的场景下适用于这种引擎。数据如果需要频繁的更新使用该引擎好（update）。对于主键查询速度也可以。搜索效率不是很高，不支持全文搜索，启动也比较慢，

MyIASM(早先)：对数据库的读操作远远多于写操作的时候，并且不需要事务支持的时候用这种引擎。如果需要频繁的insert和delete操作的时候这种引擎较好

共同点:索引都是B+树

### 说说你创建数据库时的数据库范式：你创建数据库的原则

第一范式（1NF）、第二范式（2NF）、第三范式（3NF）、巴斯-科德范式（BCNF）、第四范式(4NF）和第五范式（5NF，又称完美范式）。


常用: 第一范式:每一项都是原子性项的不可拆分，又叫无重复范式

第二范式:要求数据表中每个实例都会被唯一确定，

第三范式：如果在一个表中依赖于某个主键的字段数据就不要再出现在其他表中

### 一般从那几个方面对数据库进行优化

1). sql语句优化

尽量避免在where中使用 !=    <>(就是不等于的符号)，或者不在where中null

2). 通过索引优化：使用适当的引擎创建合适的索引

3). 数据结构优化：
范式优化:符合范式规范减少数据冗余
反范式优化：适当的增加冗余而减少使用join这样的语句
拆分表: 将不同的表进行物理分离，以减少磁盘全盘扫描的压力

4).服务器硬件优化:多花钱 

### 表的导入导出

导出:mysqldump -u root -p [-d] yourdb > file.sql  --> 加-d是只把表的数据导出

导入: mysql -u root -p mydb < file.sql --> 首先要创建自己的数据库


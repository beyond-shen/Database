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

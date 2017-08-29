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
//创建 
(1) create database databasename;  --> 创建数据库默认编码格式为ASCii
(2) create database databasename default character set utf8 collate utf8_general_ci; --> 编码格式为utf8

// 删除
drop database databasename; --> 删除数据库
```

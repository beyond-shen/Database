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

# mongodb 和mongoose

mongodb是文档型非关系型数据库，每一条记录就是一个集合

## mongodb（linux）


### 安装

### 使用以及配置

#### 配置文件位置

```shell
$ sudo vim /etc/mongo.conf
```

#### 使用

1. 默认端口是27017
2. 每次启动前需要：
```shell
$ sudo servive mongod start
```
3. 进入：
```shell
$ mongo
$ mongo ip:27017
```
4. 创建数据库，若存在切换:

```shell
$ use dbname
// 要想在show dbs看到新创建的数据库，必须在该数据库中创建一个集合并给该集合添加数据

$ db.collectionname.insert({name:'lisi',age:16})
```
5. show dbs : 显示所有数据库
6. db: 显示当前数据库
7. 数据库的删除:
```shell
db.dropDatabase()
```

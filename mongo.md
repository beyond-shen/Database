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
// 要想在show dbs看到新创建的数据库，必须在该数据库中创建一个集合并给该集合添加文档(json格式)

$ db.collectionname.insert({name:'lisi',age:16})
```
5. show dbs : 显示所有数据库
6. db: 显示当前数据库
7. 数据库的删除:
```shell
db.dropDatabase()
```
8. 显示所有集合:show collections
9. 集合的删除:
```shell
db.collectionname.drop()
//true
```
10. 文档的插入：
```
db.collectionname.insert()
db.collectionname.save() // 若是指定_id就会更新该_id的数据
```
11. 文档的查找：
```
db.collectionname.find()
db.collectionname.findOne()
```
12. 文档的更新:
```
db.collectionname.update({查询条件},{更新内容},{upsert,multi,writeConcern})

// upsert：若更新的不存在，true就是插入新记录，false就是不插入
// multi：默认false只更新找到的第一条记录，true多条更新
// writeConcern:抛出异常级别，<document>

//更新内容的常用参数:
1. $set:{} --> 重新设置
2. $unset:{age:1} --> 相当于删除指定键
3. $inc:{} --> 在对应键上增加
4. $push:{course:'html'} --> 添加一个键，给该键值是数组中添加一条数据
5. $pushAll:{course:['hello','name']} --> 给数组域中添加多条数据
6. $pop:{course:1}  --> 删除数组域中的最后一个，若为-1则是第一个，按位置
7. $pull:{course:'html'} --> 删除数组域中的指定数据
8. $pullAll:{course:['html','name']}  --> 删除数组域中指定的多条数据
9. $rename:{course:'courses'} --> 给数组域改名
10. $addToset:{} --> 数据不存在才添加
```

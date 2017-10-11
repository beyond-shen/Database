# mongodb 和mongoose

mongodb是文档型非关系型数据库，每一条记录就是一个集合

## mongodb（linux）

### 常用图形工具

[mongodb图形工具](https://robomongo.org)

### 安装

### 使用以及配置

#### 配置文件位置

```shell
$ sudo vim /etc/mongo.conf
```

#### 本地linux下操作使用

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
db.collectionname.find('age':{常用参数:值})  //查找满足条件的文档

// 常用查找参数:
1. $lt:小于
2. $lte:小于等于
3. $gt:大于
4. $gte:大于等于
5. $ne:不等于
6. $mod:[10,0] --> 能被10整除的
7. $not:{$mod:[10,0]} --> 不能被10整除的
8. $all：包含什么的
9. $size：查找指定数组长度的文档

// 按照or条件查询：$or:{[age:10,course:'html']}  --> 多个条件在一个数组里
// 按照and:多个条件用逗号隔开

db.collectionname.find().limit(2) // 限制输出2条
db.collectionname.find().skip(1) //跳过查询到的前1条文档
db.collectionname.find().count() // 统计文档个数
db.collectionname.find().sort() // 按照条件进行排序
db.collectionname.find({},{'name':1}) // 查询到的文档按照指定域输出
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
13. 文档的删除:
```
db.collectionname.remove({query},{justOne:boolean,writeConcern:<document>})
//query:删除指定条件的文档
// justOne: 设置为true或者１时，仅仅删除第一个符合条件的文档, 默认删除所有符合条件的
```
14. 索引（是对值进行排序的一种结构）：
```
db.collectionname.ensureIndex({name:1,age:-1}) // 创建索引，1为升序，-1为降序
db.collectionName.ensureIndex({"name": 1}, {"unique": true}) //创建name域不可以有重复值，唯一索引
db.collectionName.dropIndex({"name":1}) // 删除指定索引
db.collectionName.dropIndexes() // 删除所有索引
```
#### 远程数据库的使用

远程数据库地址:[网络数据库](mlab.com)

[mongodb api文档](http://mongodb.github.io/node-mongodb-native/2.2/api/)

1. 安装mongob第三方包
```shell
$ npm install mongodb --save-dev
$ npm i mongodb -d
```
2. 连接mongodb数据库:创建xx.js

```js
var MongoClient = require('mongodb').MongoClient;

// 本地的url写法
var url = 'mongodb://ip:27017/databasename';

// 数据库的连接
MongoClient.connect(url,function(err,db){
  // 对指定集合文档的插入
  db.collection('collectionname').insert({})
  // 对指定集合文档的查询
  var curosr = db.collection('collectionname').find() // 得到的不是数据而是迭代对象
  // 得到文档
  cursor.each(function(err,doc){
    if(doc != null){
     console.log(doc);
    }
  })
  db.close()
});
```

## mongoose

mongoose是一个提供了MongoDB地的相映射的Node.js库，将数据库中的数据转换为js对象来使用，是用来连接nodejs和MongoDB的一种中间件

### 使用

#### 安装

```shell
$ npm install mongoose --save
```

#### 使用mongoose连接数据库

必须确保MongoDB处于运行中
```js
var mongoose = require('mongoose');
var url = 'mongodb://ip:27017/dbname';
mongoose.connect(url,{useMongoClient:true});
var db = mongoose.connection;
```
#### 使用mongoose.Schema方法定义数据集格式，

Schema仅仅只是数据属性的模型，以文件形式存储但不具备数据库的操作能力

```js
var Schema = mongoose.Schema; // 获得mongoose中的内置Schema
// 通过new来创建一个指定的数据属性模型
var userSchema = new Schema({
  name: String,
  age:Number
})
```

#### 使用mongoose.model将格式分配给指定数据集

将Schema发布为model,模型变量名首字母大写

```js
// 给指定集合指定的数据属性模型,mongoose会给指定的集合名加上复数，若是复数则不加
var User = mongoose.model('User',userSchema);
```
#### model创建实例

var wang = new User({
 name:'wangsan',
 age:16,
})

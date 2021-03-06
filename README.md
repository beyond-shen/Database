# Database
关于各种数据库的介绍和使用

数据库系统DBS:由数据库，数据库管理系统和应用开发工具构成

数据库管理系统DBMS:是一个软件，操纵和管理数据库的大型软件，保证数据库的安全性和完整性

数据库DB:按照数据结构来组织、存储和管理数据的仓库。数据库是在数据库管理系统管理和控制之下，存放在存储介质上的数据集合。

## 数据库建表规范

### 表名规范

1. 以模块或者系统为前缀，前缀全部大写或者首字母大写，表名以大写字母开头
1. 以英文单词或者缩写来命名，不要太长，尽量用单数形式
1. 后台表名加后缀_b
1. 备份时加后缀为_bak


### 表字段规范

1. 字段名用可表示意义的英文单词来命名，但是不要取关键词或者数据类型
2. 作唯一标识的字段为id,类型为Int或者长整型
3. 所有业务内的编号字段用code来命名，比如wf_code
4. 不要重复表名



## 关系型数据库

### 概念

采用了关系模型来组织数据的数据库

### 瓶颈

1. 高并发读写需求

2. 海量数据的高效率读写

3. 高扩展性和可用性

### 常用

Oracle,Mysql,sQlite3,sqlServer,DB2

## 非关系型数据库 NoSQL

### 概念和分类

#### 键值存储数据库

#### 列存储数据库

#### 文档型数据库

文档型数据库的灵感是来自于Lotus Notes办公软件的，而且它同第一种键值存储相类似。该类型的数据模型是版本化的文档，半结构化的文档以特定的格式存储，比如JSON。文档型数据库可 以看作是键值数据库的升级版，允许之间嵌套键值。而且文档型数据库比键值数据库的查询效率更高

#### 图形数据库

### 试用场景

1. 数据模型比较简单
2. 需要灵活性更强的IT系统；
3. 对数据库性能要求较高；
4. 不需要高度的数据一致性；
5. 对于给定key，比较容易映射复杂值的环境。

###  mongodb 和模块 mongoose


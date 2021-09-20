# 索引

## 索引的优点

- 索引大大减小了服务器需要扫描的数据量
- 索引可以帮助服务器避免排序和临时表
- 索引可以将随机 IO 变成顺序 IO
- 索引对于 InnoDB（对索引支持行级锁）非常重要，因为它可以让查询锁更少的元组。

在 MySQL5.1 和更新的版本中，InnoDB 可以在服务器端过滤掉行后就释放锁，但在早期的 MySQL 版本中，InnoDB 直到事务提交时才会解锁。对不需要的元组的加锁，会增加锁的开销，降低并发性。 InnoDB 仅对需要访问的元组加锁，而索引能够减少 InnoDB 访问的元组数。但是只有在存储引擎层过滤掉那些不需要的数据才能达到这种目的。一旦索引不允许 InnoDB 那样做（即索引达不到过滤的目的），MySQL 服务器只能对 InnoDB 返回的数据进行 WHERE 操作，此时，已经无法避免对那些元组加锁了。如果查询不能使用索引，MySQL 会进行全表扫描，并锁住每一个元组，不管是否真正需要。
关于 InnoDB、索引和锁：InnoDB 在二级索引上使用共享锁（读锁），但访问主键索引需要排他锁（写锁）

## 缺点

虽然索引大大提高了查询速度，同时却会降低更新表的速度，如对表进行 INSERT、UPDATE 和 DELETE。因为更新表时，MySQL 不仅要保存数据，还要保存索引文件。

建立索引会占用磁盘空间的索引文件。一般情况这个问题不太严重，但如果你在一个大表上创建了多种组合索引，索引文件的会膨胀很快。

如果某个数据列包含许多重复的内容，为它建立索引就没有太大的实际效果。

对于非常小的表，大部分情况下简单的全表扫描更高效；

索引只是提高效率的一个因素，如果你的 MySQL 有大数据量的表，就需要花时间研究建立最优秀的索引，或优化查询语句。

因此应该只为最经常查询和最经常排序的数据列建立索引。

MySQL 里同一个数据表里的索引总数限制为 16 个。

## Mysql 建立索引类型

- 单列索引: 即一个索引只包含单个列，一个表可以有多个单列索引，但这不是组合索引

- 组合索引: 即一个索包含多个列

索引是在存储引擎中实现的，而不是在服务器层中实现的。所以，每种存储引擎的索引都不一定完全相同，并不是所有的存储引擎都支持所有的索引类型。

### 索引分类

- 普通索引 index: 加速查找

- 唯一索引
  主键索引:primary key 加速查找 + 约束(不为空且唯一)
  唯一索引: unique 加速查找+约束(唯一)

- 联合索引
  primary key(id,name) :联合主键索引
  unique(id,name):联合唯一索引
  index(id,name):联合普通索引

- 全文索引
  full text: 用于搜索很长一篇文章的时候,效果最好

- 空间索引
  spatial:了解就好，几乎不用

### 索引创建和删除方式:

- 创建删除索引的语法

```bash

#方法一：创建表时
CREATE TABLE 表名 (
  字段名1  数据类型 [完整性约束条件…],
  字段名2  数据类型 [完整性约束条件…],
  [UNIQUE | FULLTEXT | SPATIAL ]   INDEX | KEY
  [索引名]  (字段名[(长度)]  [ASC |DESC])
  );


#方法二：CREATE在已存在的表上创建索引
  CREATE  [UNIQUE | FULLTEXT | SPATIAL ]  INDEX  索引名
    ON 表名 (字段名[(长度)]  [ASC |DESC]) ;


#方法三：ALTER TABLE在已存在的表上创建索引
  ALTER TABLE 表名 ADD  [UNIQUE | FULLTEXT | SPATIAL ] INDEX
    索引名 (字段名[(长度)]  [ASC |DESC]) ;

#删除索引：DROP INDEX 索引名 ON 表名字;

DROP INDEX 索引名 ON 表名字;

```

- 实例

```bash

善用帮助文档
help create
help create index
==================
1.创建索引
    -在创建表时就创建（需要注意的几点）
    create table s1(
    id int ,#可以在这加primary key
    #id int index #不可以这样加索引，因为index只是索引，没有约束一说，
    #不能像主键，还有唯一约束一样，在定义字段的时候加索引
    name char(20),
    age int,
    email varchar(30)
    #primary key(id) #也可以在这加
    index(id) #可以这样加
    );
    -在创建表后在创建
    create index name on s1(name); #添加普通索引
    create unique age on s1(age);添加唯一索引
    alter table s1 add primary key(id); #添加住建索引，也就是给id字段增加一个主键约束
    create index name on s1(id,name); #添加普通联合索引
2.删除索引
    drop index id on s1;
    drop index name on s1; #删除普通索引
    drop index age on s1; #删除唯一索引，就和普通索引一样，不用在index前加unique来删，直接就可以删了
    alter table s1 drop primary key; #删除主键(因为它添加的时候是按照alter来增加的，那么我们也用alter来删)

```

### 索引失效

在模糊查询的时候,第一个通配符使用的就是%.这个时候索引是失效的。

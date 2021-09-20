# 约束

约束实际上就是表中数据的限制条件

## 约束作用

> 表在设计的时候加入约束的目的就是为了保证表中的记录完整和有效

- 比如 name 字段中要让其用户名不重复,就需要添加约束,或者必须注册的时候需要添加邮箱等等

## 约束种类

- 非空约束(not null)

- 唯一性约束(unique)

- 主键约束(primary key) PK

- 外键约束(foreign key) FK

## 非空约束

> 用 not null 约束的字段不能为 null 值 必须给定具体的数据

### 创建表的时候加入非空约束

- 创建用户表,用户名不能为空

```bash

	mysql> create table t_user(
    -> id int(10),
    -> name varchar(32) not null
    -> );
Query OK, 0 rows affected (0.08 sec)

```

### 如果没有插入 name 字段数据则会报错

```bash
mysql> insert into t_user (id) values(1);
ERROR 1364 (HY000): Field 'name' doesn't have a default value

```

## 唯一性约束

> unique 约束的字段,具有唯一性,不可重复,但可以为 null

### 创建表,保证邮箱地址唯一(列级节约)

```bash
mysql> create table t_user(
    -> id int(10),
    -> name varchar(32) not null,
    -> email varchar(128) unique
    -> );
Query OK, 0 rows affected (0.03 sec)

```

### 表级约束

```bash
mysql> create table t_user(
    -> id int(10),
    -> name varchar(32) not null,
    -> email varchar(128），
	-> unique(email)
    -> );
```

如果插入相同的 email 则会报错

```bash
mysql> insert into t_user(id,name,email) values(1,'xlj','932834897@qq.com');
Query OK, 1 row affected (0.00 sec)

mysql> insert into t_user(id,name,email) values(2,'jay','932834897@qq.com');
ERROR 1062 (23000): Duplicate entry '932834897@qq.com' for key 'email'

```

## 主键约束

> 表设计的时候一定要有主键

### 主键涉及术语

- 主键约束

- 主键字段

- 主键值

### 以上三种术语关系

> 表中的某个字段添加主键约束后，该字段为主键字段，主键字段中出现的每一个数据都称为主键值

### 主键约束与 "not null unique" 区别

> 给某个字段添加主键约束后，该字段不能重复也不能为空,效果和'not null unique'约束相同,但本质不同

> 主键约束除了可以做到'not null unique' 还会默认添加索引---'index'

### 一张表应该有主键字段,如果没有表示该表无效

- 主键值: 是当前数据的唯一标识,是当前数据的身份证号

- 即使表中两行记录相关数据相同,但由于主键值不同,所以也认为是两行不同的记录

### 按主键约束的字段数量分类

> 无论是单一主键还是复合主键,一张表主键约束只能有一个

### 单一主键(列级定义)

```bash
mysql> create table t_user(
    -> id int(10) primary key,
    -> name varchar(32)
    -> );
Query OK, 0 rows affected (0.07 sec)

```

### 单一主键(表级定义)

```bash
mysql> create table t_user(
    -> id int(10),
    -> name varchar(32) not null,
    -> constraint t_user_id_pk primary key(id)
    -> );
Query OK, 0 rows affected (0.01 sec)

```

### 自增

- 在 MySQL 数据库提供了一个自增的数字，专门用来自动生成主键值，主键值不用用户维护，自动生成，自增数从 1 开始，以 1 递增(auto_increment)

```bash
mysql> create table t_user(
    -> id int(10) primary key auto_increment,
    -> name varchar(32) not null
    -> );
Query OK, 0 rows affected (0.03 sec)

```

- 插入两行 主键值会增加

```bash

mysql> insert into t_user(name) values('jay');
Query OK, 1 row affected (0.04 sec)

mysql> insert into t_user(name) values('man');
Query OK, 1 row affected (0.00 sec)

mysql> select * from t_user;
+----+------+
| id | name |
+----+------+
|  1 | jay  |
|  2 | man  |
+----+------+
2 rows in set (0.00 sec)

```

## 外键

### 什么是外键

若有两个表 A、B，id 是 A 的主键，而 B 中也有 id 字段，则 id 就是表 B 的外键，外键约束主要用来维护两个表之间数据的一致性。

A 为基本表，B 为信息表

### 外键涉及到的术语

- 外键约束

- 外键字段

- 外键值

### 外键约束,外键字段,外键值之间的关系

某个字段添加外键约束之后，该字段称为外键字段，外键字段中每个数据都是外键值

### 一张表可以有多个外键(与主键不同)

### 注意点

- 外键值可以为 null

- 外键字段去引用一张表的某个字段的时候，被引用的字段必须具有 unique 约束

- 有了外键引用之后，表分为父表和子表

- 班级表：父表

- 学生表：子表

- 创建先创建父表

- 删除先删除子表数据

- 插入先插入父表数据

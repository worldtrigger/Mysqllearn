# 表的操作

## 学习要点

- 表通过 CREATE TABLE 语句创建而成

- 表和列的命名要使用有意义的文字

- 指定列的数据类型(整数型,字符型和日期型等)

- 可以在表中设置约束(主键约束和 NOT NULL 来约束)

## 数据库的创建

- 创建数据库

```bash

CREATE DATABASE <数据库名>

```

- 举例

```bash

CREATE DATABASE shop;

```

## 表的创建

- 创建表

```bash

CREATE TABLE <表名>
(
  <列名1> <数据类型> <该列所需约束>,
  <列名2> <数据类型> <该列所需约束>,
  <列名3> <数据类型> <该列所需约束>,
  <列名4> <数据类型> <该列所需约束>,
  <列名5> <数据类型> <该列所需约束>,
  <列名6> <数据类型> <该列所需约束>,
  .
  .
  <该表的约束1>,<该表的约束2>,...
)

```

> 该语法清楚的描述了我们要创建一个包含<列名 1>,<列名 2>,...的名称为<表名>的表,非常容易理解

> 每一列的数据类型(后述)是必须要指定的,还要为需要的列设置约束(后述)。约束可以在定义列的时候进行设置,也可以在语句的末尾设置

- 举例

```bash

CREATE TABLE Product
(
  product_id CHAR(4)  NOT NULL,
  product_name VARCHAR(100) NOT NULL,
  product_type VARCHAR(32) NOT NULL,
  sale_price INTEGER,
  purchase_price INTEGER,
  regist_date DATE,
  PRIMARY KEY (product_id)
)

```

### 命名规则

- 我们只能使用半角英文字母,数字,下划线(\_)作为数据库,表和列的名称

> 数据库名称,表名和列名可以使用以下三种字符 1.半角英文字符 2.半角数字 3 下划线

`名称必须以半角英文字母作为开头`

- 名称不能重复

`在一个数据库里面表名绝对不能重复`

- 商品表和 Product 表对应的关系

| 商品表中的列名 | Product 表定义的列名 |
| -------------- | -------------------- |
| 商品编号       | product_id           |
| 商品名称       | product_name         |
| 商品种类       | product_type         |
| 销售单价       | sale_price           |
| 进货单价       | purchase_price       |
| 登记日期       | regist_date          |

### 数据类型的指定

所有列都必须指定数据类型

数据类型的种类包含(数字型,字符型,日期型)每一列都不能存储与该列数据类型不符的数据。声明为整数型的列不能存储'abc'这样的字符串

常用的也就 4 种类型

- INTEGER 类型

用来存储整数的列的数据类型(数字型),不能存小数

- CHAR 类型

字符串的缩写,用来指定存储字符串列的数据类型。例如 CHAR(8)
它是定长,假如存的是'abcd'那后面就是 4 位空格类似 'abcd 空格 空格 空格 空格'

`特别注意的就是Mysql是不分大小写的,但是里面的数据是区分大小写的,abc和ABC不同`

- VARCHAR 型号

同 CHAR 一样 他也表示字符串类型只不过他是可变字符串长度

输入'abc'保存的就是'abc'

- DATE 型

用来指定存储的(年月日)的列的数据类型(日期型)

### 约束的设置

约束 是除了数据类型之外,对列中存储的数据进行限制或者追加条件的功能

- 第一种

上表中有两种约束 NOT NULL 表示不能输入空白,必须要数据数据

- 第二种

用来给 product_id 列设置主键约束的

```bash
PRIMARY KEY (product_id)
```

### 表的删除(DROP TABLE)

- 删除表

```javascript

DROP TABLE <表名>;

```

- 例子

```javascript

DROP TABLE Product;

```

> 删除了的表是无法恢复的,删除前请仔细确认

### 表的更新(ALTER TABLE 语句)

`添加列`

```javascript

ALTER TABLE <表名> ADD COLUMN <列的定义>

```

- 例子

```javascript

ALTER TABLE Product ADD COLUMN product_name_pinyin VARCHAR(100);

```

`删除列`

```javascript

ALTER TABLE <表名> DROP COLUMN <列名>;


```

`表改名`

- 通常在 RNAME 之后按照<变更前的名称>,<变更后的名称>的顺序来指定表的名称

```javascript

RENAME TABLE Product to Product1;

```

> 表定义变更后无法恢复,执行前请仔细确认

### 数据库使用步骤

- 连接数据库

- 查看数据库

```bash

show databases

```

- 使用数据库

```bash

use 数据库名

```

- 查看使用表

```bash

show tables

```

- 查看表的结构

```bash

desc <表的名字>

```

- 查看正在使用的数据库

```bash

select database();

```

- 查看正在使用的数据库版本

```bash

select version();

```

- 结束或者终止 Mysql 命令

```bash

\c

```

- 退出命令

```bash

exit

```

# 数据插入

## 学习重点

- 使用 INSERT 语句可以向表中插入数据(行).原则上 INSERT 语句每次执行一行数据的插入

- 将列名和值用逗号隔开,分别括在()内,这种形式称为清单

- 对表中所有列进行 INSERT 操作时可以省略表名后的列清单

- 插入 NULL 时候 需要在 VALUES 子句的值清单写入 NULL

- 可以为表中的列设定默认值(初始值),默认值可以通过在 CREATE TABLE 语句中指定 DEFAULT 关键字(显示方法)或省略列清单(隐式方法)

- 使用 INSERT...SELECT 可以从其他表中复制数据

## INSERT 数据插入

### 语法结构

```bash

INSERT INTO <表名> (列1,列2,列3) VALUES (值1,值2,值3)

```

- 例子

```bash

INSERT INTO ProductIns (product_id, product_name, product_type, 
sale_price, purchase_price, regist_date) VALUES ('0001', 'T恤衫', 
'衣服', 1000, 500, '2009-09-20');

```

将列名和值用逗号隔开,分别括在()内。这种形式称为清单。

1. 列清单

```bash
 (product_id, product_name, product_type,
sale_price, purchase_price, regist_date)
```

2. 值清单

```bash
 ('0001', 'T恤衫', '衣服', 1000, 500,'2009-09-20')
```

3. 当然表名后面的列清单和值清单的列数必须保持一致.列数不一致会出错,无法插入

> 原则上执行 INSERT 语句会插入一行数据.因此插入多行的时候,需要循环执行

### 多行 INSERT 插入

```bash

INSERT INTO ProductIns VALUES ('0002', '打孔器','办公用品', 500, 320, '2009-09-11'),('0003', '运动T恤','衣服', 4000, 2800, NULL),('0004', '菜刀','厨房用具', 3000, 2800, '2009-09-20');

```

首先，INSERT 语句的书写内容及插入的数据是否正确。若不正确会发生
INSERT 错误，但是由于是多行插入，和特定的单一行插入相比，想要找出到底是
哪行哪个地方出错了，就变得十分困难

### 列清单的省略

要是全表插入,则可以省略表名后的列清单.这时 VALUES 会默认从左到右的顺序赋值给每一列。

```bash

-- 包含列清单
INSERT INTO ProductIns (product_id, product_name, product_type, 
sale_price, purchase_price, regist_date) VALUES ('0005', '高压锅', 
'厨房用具', 6800, 5000, '2009-01-15');
-- 省略列清单
INSERT INTO ProductIns VALUES ('0005', '高压锅', '厨房用具', 
6800, 5000, '2009-01-15');

```

### 插入 NULL

- 想要插入的 NULL 列一定不能设置 NOT NULL 约束。

- 插入失败不会影响以前已经插入的数据

```bash

INSERT INTO ProductIns (product_id, product_name, product_type,sale_price, purchase_price, regist_date) VALUES ('0006', '叉子','厨房用具', 500, NULL, '2009-09-20');

```

### 插入默认值

我们还可以向表中插入`默认值`(初始值) 也可以在创建表中设置 DEFAULT 约束来设定默认值

创建表的时候 如下:

```bash

CREATE TABLE ProductIns
(product_id CHAR(4) NOT NULL,
 （略）
 sale_price INTEGER DEFAULT 0, -- 销售单价的默认值设定为0;
 （略）
 PRIMARY KEY (product_id));

```

- 通过显式的方法插入数据

```bash

INSERT INTO ProductIns (product_id, product_name, product_type,sale_price, purchase_price, regist_date) VALUES ('0007','擦菜板', '厨房用具', DEFAULT, 790, '2009-04-28');

```

因为创建表的时候设置默认值，那么插入的时候可以直接写 DEFAULT 即可

### 从其他表中复制数据

> 插入的数据后面要是有 SELECT 则没有 VALUES

- 第一种方法全部插入列名都一样

```bash

INSERT INTO 新表 SELECT * FROM 旧表

```

- 第二种方法(列名不一样)

```bash

INSERT INTO 新表(字段1,字段2,.......) SELECT 字段1,字段2,...... FROM 旧表

```

```bash

-- 将商品表中的数据复制到商品复制表中
INSERT INTO ProductCopy (product_id, product_name, product_type, 
sale_price, purchase_price, regist_date)
SELECT product_id, product_name, product_type, sale_price, 
purchase_price, regist_date
 FROM Product;

```

> INSERT 语句的 SELECT 语句中，可以使用 WHERE 子句或者 GROUP BY 子句等任何 SQL 语法（但使用 ORDER BY 子句并不会产生任何效果）。

## 表的复制以及批量插入

### 表的复制

- 将查询结果当作表创建

```bash

create table 新表 as select * from 复制表;

```

- 将查询结果插入到一张表中

```bash

insert into 表名 select * from 复制表

```

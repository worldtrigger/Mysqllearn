# 查询基础

## 本节知识

```bash

- 使用SELECT 语句从表中读取数据
- 将列设定显示用的别名
- SELECT语句可以使用常数或者表达式
- 通过DISTINCT可以删除重复的行
- SQL可以用于注释
- 可以通过WHERE语句从表中选取出符合查询条件的数据

```

## 列的查询

从表中选取数据的时候 我们需要使用 SELECT 语句.通过 SELECT 语句 查询并选取出必要的数据过程 称为 `匹配查询`或者`查询`

### 基本的 SELECT 语句

```javascript
SELECT <列名> FROM <表名>;
```

该 SELECT 语句包含了 SELECT 和 FROM 两个子句。子句都是 SQL 语句的组成要素,是以 SELECT 或者 FROM 等作为起始的短语

SELECT 子句中列举了希望从表中查询出列的名称,而 FROM 子句则指定了选取出数据的表的名称

- 例如

```bash

SELECT name,price,id  FROM Product;

```

> 查询结果中列的顺序和 SELECT 子句中的顺序相同

### 查询表中所有的列

```bash

SELECT * FROM <表名>;

```

> - 星号就代表全部列的意思

`如果使用*星号就无法设定列的显示顺序`

### 为列设定别名

- SQL 语句可以使用 AS 关键字为列设定别名

```bash

SELECT product_id AS id, product_name AS name FROM product;

```

- 别名可以使用中文，使用中文时需要用双引号("")括起来,特别注意不是`单引号`

```bash

SELECT product_id AS "商品ID",product_name AS "商品名称" FROM product;

```

### 常数的查询

- 当查询的时候有的时候为了方便看需要补充列。这个时候需要常数了

```bash

SELECT '商品' AS string, 38 AS number,'2009-12-12' AS date,id,name FROM product;

```

### 从结果中删除重复行

- 在 SELECT 语句中 DISTINCT 来实现

```bash

SELECT DISTINCT name FROM product;

```

> 在使用 DISTINCT 时候,NULL 也被视为一类数据,NULL 存在于多行中,也会被合并为一条数据

- 在多列之前使用 DISTINCT,

这几列条件必须都满足,有一条不满足也不会去除

```javascript

SELECT DISTINCT name,date FROM product;

```

`DISTINCT 关键字只能用在第一个列名之前`

### 根据 WHERE 条件来选择记录

- 在 SELECT 语句中通过 WHERE 来指定查询数据的条件

```bash

SELECT <列名>,...FROM <表名> WHERE <条件表达式>

```

例如

```bash

SELECT id,name,age from product WHERE price='27.36'

```

> WHERE 子句就是用来查询条件表达式 等号就是比较两边的内容是否相等

`SQL语句的书写顺序是固定的,不能随意更改`

`WHERE 子句必须紧跟在 FROM 之后`

### 注释的书写方法

- 1 行注释

书写在"--" 之后,只能写在同一行

```bash

-- 本SELECT语句会从结果中删除重复行。
SELECT DISTINCT product_id, purchase_price
 FROM Product;

```

- 多行注释

书写在 "/" 和 "/" 之间,可以跨多行。

```bash
/* 本SELECT语句，
会从结果中删除重复行。*/
SELECT DISTINCT product_id, purchase_price
FROM Product;
```

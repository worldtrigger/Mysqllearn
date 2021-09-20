# 子查询

## 学习重点

- 子查询就是一次性视图(SELECT 语句),与视图不同的是子查询在 SELECT 语句执行完毕之后消失

- 由于子查询需要命名,因此需要根据处理内容来指定恰当的名称

- 标量子查询就是只能返回一行一列的子查询

## 子查询就是定义视图的 SELECT 语句

> 括号里就是子查询语句

- 举例

```bash

SELECT product_type, cnt_product
 FROM ( SELECT product_type, COUNT(*) AS cnt_product
 FROM Product
 GROUP BY product_type ) AS ProductSum;

```

执行顺序:首先会执行 FROM 子句中的 SELECT 语句。然后才会执行外层的 SELECT 语句

- 第一步

```bash

1. SELECT product_type, COUNT(*) AS cnt_product FROM Product GROUP BY product_type

```

- 第二步

```bash

2.SELECT product_type, cnt_product FROM ProductSum;

```

> 子查询会优先执行

## 增加子查询的层数

由于子查询的层数原则上没有限制，因此可以像“子查询的 FROM 子
句中还可以继续使用子查询，该子查询的 FROM 子句中还可以再使用子查
询……”这样无限嵌套下去

> 它优先执行执行的就是最内部的子查询

```bash

SELECT product_type, cnt_product
 FROM (SELECT *
 FROM (SELECT product_type, COUNT(*) AS cnt_product
 FROM Product
 GROUP BY product_type) AS ProductSum -------①
 WHERE cnt_product = 4) AS ProductSum2; -----②

```

## 子查询的名称

原则上子查询必须有别名,为子查询设定名称时候需要用 AS 关键字,该关键字也可以省略

## 标量子查询

标量就是单一的意思。标量子查询就是有一个特殊的限制,那就是必须而且只能返回一行一列的结果.
也就是返回表中某一行的某一列的值 例如'10'或者'北京'这样的值

> 标量子查询就是返回单一值的子查询

- 例如

```bash

SELECT product_id, product_name, sale_price
 FROM Product
 WHERE sale_price > (SELECT AVG(sale_price)
 FROM Product);

```

括号里面的查询就是标量子查询因为他只返回一个结果

## 标量子查询的书写位置

标量子查询的书写位置并不仅仅局限于 WHERE 子句中，通常任何可
以使用单一值的位置都可以使用。也就是说，能够使用常数或者列名的
地方，无论是 SELECT 子句、GROUP BY 子句、HAVING 子句，还是
ORDER BY 子句，几乎所有的地方都可以使用。

```bash

SELECT product_id,
 product_name,
 sale_price,
 (SELECT AVG(sale_price)
 FROM Product) AS avg_price
 FROM Product;

```

## 关联子查询

> 就是在子查询中添加 WHERE 的子句条件。在使用关联子查询的时候,需要在表对应的列名之前加上表的别名,以<表名>,<列名>的形式记录

`当你的子查询出现了多条数据。而前面又有where语句的时候(一对一的关系)这个时候就必须要和全面的主表做一个关联。把子查询变成1对1的关系`

例如:

```bash

SELECT product_type, product_name, sale_price
 FROM Product AS P1 ①
 WHERE sale_price > (SELECT AVG(sale_price)
 FROM Product AS P2 ②
 WHERE P1.product_type = P2.product_typei
 GROUP BY product_type);

```

这里的 P2 查询的不是平均数了.而是带有 type,name,saleprice 的一个集合

`特别注意的就是关联条件必须写在条件内部,只能在子查询里面变化`

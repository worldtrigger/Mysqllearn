# 对查询结果进行排序

## 学习重点

- 使用 ORDER BY 子句对查询结果进行排序

- 使用 ORDER BY 子句中列名的后面使用关键字 ASC 可以进行升序排序,使用 DESC 关键字降序排列

- ORDER BY 子句中可以指定多个排序键

- 排序键中包含 NULL 时,会在开头或者末尾进行汇总

- ORDER BY 子句中可以使用 SELECT 子句中定义的列的别名。

- ORDER BY 子句中可以使用 SELECT 子句中未出现的列或者聚合函数

- ORDER BY 子句中不能使用列的编号

## ORDER BY 子句

### 语法结构

```bash

SELECT <列名1>,<列名2> FROM <表名> ORDER BY <排序基准列1>,<排序基准列2>...;

```

- 举例

```bash
SELECT product_id, product_name, sale_price, purchase_price
 FROM Product
ORDER BY sale_price;
```

### 执行顺序

```bash

SELECT 子句----> FROM 子句---> WHERE子句----> GROUP BY子句-----> HAVING子句 ----> ORDER BY 子句

```

## 指定升序或者降序

- 降序排列 DESC,升序排列 ASC

```bash

SELECT product_id, product_name, sale_price, purchase_price
 FROM Product
ORDER BY sale_price DESC;

```

> 未指定 ORDER BY 子句中排列顺序时会默认使用升序进行排列。

## 指定多个排序键

规则是优先使用左侧的键,如果该列存在相同值的话，在接着参考右边的键

```bash
SELECT product_id, product_name, sale_price, purchase_price
 FROM Product
ORDER BY sale_price, product_id;
```

## NULL 的顺序

> 排序键中包含 NULL 时,会在开头或者末尾汇总

```bash

SELECT product_id, product_name, sale_price, purchase_price
 FROM Product
ORDER BY purchase_price;

```

## 在排序键中使用显示用的别名

- 例如

```bash

SELECT product_id AS id, product_name, sale_price AS sp, purchase_price
 FROM Product
ORDER BY sp, id;

```

## ORDER BY 子句中可以使用的列

ORDER BY 子句中也可以使用存在于表中、但并不包含在 SELECT
子句之中的列

```bash

SELECT product_name, sale_price, purchase_price
 FROM Product
ORDER BY product_id;

```

- 除此之外还可以使用聚合函数

```bash

SELECT product_type, COUNT(*)
 FROM Product
 GROUP BY product_type
ORDER BY COUNT(*);

```

# 数据的更新

## UPDATE 基础语法

- 语法

```bash

UPDATE <表名> SET <列名> = <表达式>;

```

- 例子

```bash

UPDATE Product SET regist_date = '2009-10-10';

```

> 这种语句这样写很危险，他会把全表的那个列都修改成一个值

`所以使用UPDATE 后面必须接WHERE`

## 指定条件的 UPDATE 语句

- 语法

```bash

UPDATE <表名> SET <列名> = <表达式>,<列名2> =<表达式> WHERE <条件>;

```

## 多列更新

- 语法

```bash

UPDATE Product
 SET sale_price = sale_price * 10,
 purchase_price = purchase_price / 2
 WHERE product_type = '厨房用具';

```

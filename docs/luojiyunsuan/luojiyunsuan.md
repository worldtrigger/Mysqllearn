# 逻辑运算符

## 学习重点

- 通过使用逻辑运算符,可以将多个查询条件进行组合

- 通过 NOT 运算符可以生成"不是~"这样的查询条件

- 两边条件都成立时,使用 AND 运算符的查询条件成立

- 只要两边的条件中有一个成立,使用 OR 运算符的查询条件就可以成立

- 值可以归结为真(TRUE)和假(FALSE)其中之一的值为真值.比较运算符在比较成立的时候返回真,不成立返回假

- 将根据逻辑运算符对真值进行的操作及其结果汇总成的表称为真值表

## NOT 运算符

NOT 不能单独使用,必须和其他查询条件组合起来使用.

```bash

SELECT id,name,price FROM product WHERE NOT price >=1000;

```

这样查询的结果就是 price 小于 1000

## AND 运算符 和 OR 运算符

- 在 WHERE 子句中使用 AND 运算符和 OR 运算符,可以对多个查询条件进行组合

### AND 运算符

AND 运算符在其两侧的查询条件都成立时,整个查询条件才成立.其意思相当于'并且'

```bash

SELECT id,name from product WHERE type='雨衣' AND price >1000;

```

必须同时满足两个条件 一个是类型是雨衣并且价格比 1000 大

### OR 运算符

```bash

SELECT name,price FROM product WHERE type='雨衣' OR price >1000;

```

只需要满足一个条件即可 类型 是雨衣 或者价格 比 1000 大

### 优先级

AND 的优先级 比 OR 大

例如:

```bash

SELECT product_name, product_type, regist_date
 FROM Product
 WHERE product_type = '办公用品'
 AND regist_date = '2009-09-11'
 OR regist_date = '2009-09-20';

```

这个时候看条件会被解析成

```bash
「product_type = '办公用品' AND regist_date = '2009-09-11'」
OR
「regist_date = '2009-09-20'」
```

`所以一般情况加括号来突出优先级`

```bash

SELECT product_name, product_type, regist_date
 FROM Product
 WHERE product_type = '办公用品'
 AND ( regist_date = '2009-09-11'
 OR regist_date = '2009-09-20');

```

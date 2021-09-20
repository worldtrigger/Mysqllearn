# 算术运算符和比较运算符

## 学习重点

- 运算符就是对其两边的列或者值进行运算(计算或者比较大小等)的符号

- 使用算术运算符可以进行四则运算

- 括号可以提升运算的优先顺序(优先进行运算)

- 包括 NULL 的运算,其结果也是 NULL

- 比较运算符可以用来判断列或者值是否相等,还可以用来比较大小

- 判断是否为 Null,需要用 IS NULL 或者 IS NOT NULL 运算符

## 算术运算符

比如结果乘以 2

```bash

SELECT price*2 AS "sale_priceX2"

```

- SQL 语句中的四则运算

```bash

加法运算  +

减法计算  -

乘法计算  *

除法计算  /

```

- SQL 语句中也可以使用括号(),括号中会优先得到提升

## 需要注意 NULL

比如 5 + NULL ,10-NULL, 4/NULL

`所有包含NULL的计算,结果肯定是NULL`

`NULL除以0还是NULL`

`5除以0会发生错误`

## 比较运算符

- 比较运算符汇总

```bash

= 等于

<> 不等于

> 大于

< 小于

>= 大于等于

<= 小于等于
```

- 例如

```bash

SELECT id,name FROM product WHERE id <> 3;

SELECT date,name FROM product WHERE id>=5；

```

- 这里特别备注

```bash

在Mysql里面字符串2和数字2不是一码事。不能在Mysql中排序

例如 '11'确实比'2'小

```

### 不能对 NULL 使用比较运算符

- 要取出 NULL 的记录

```bash

SELECT id,price FROM product WHERE name IS NULL;

```

- 要取出非 NULL 的记录

```bash

SELECT id,price FROM product WHERE name IS NOT NULL;

```

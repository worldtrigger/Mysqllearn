# 谓词

```bash

通俗来讲谓词就是函数中的一种，是需要满足特定条
件的函数，该条件就是返回值是真值。对通常的函数来说，返回值有可能
是数字、字符串或者日期等，但是谓词的返回值全都是真值（TRUE/
FALSE/UNKNOWN）。这也是谓词和函数的最大区别。

```

本节会介绍以下谓词

- LIKE

- BETWEEN

- IS NULL, IS NOT NULL

- IN

- EXISTS

## Like(模糊查询)

`LIKE查询一般都跟%`

### 实例化

- 必须开头满足 ddd 后面无所谓的字符串

```bash
SELECT *
 FROM SampleLike
 WHERE strcol LIKE 'ddd%';
```

> 其中的 % 是代表“0 字符以上的任意字符串”的特殊符号，本例中代表“以 ddd 开头的所有字符串”。

- 中间一致查询就是

```bash

SELECT * FROM product WHERE name LIKE '%ddd%';

```

- 后方一致查询就是

```bash
SELECT * FROM product WHERE name LIKE '%ddd';
```

> 有的时候我们需要单独一位占据位置就是 \_ 来占位

- 例如

```bash
SELECT * FROM product WHERE name LIKE '_ddd';
```

就表示查找 4 位的字符串 后三位结尾是 ddd 的

## BETWEEN

- 使用 BETWEEN 必须和 AND 连接, 表示在一个区间(包前又包后)

- 如果不想包含临界值就只能使用大于和小于号

```bash

SELECT product_name, sale_price
 FROM Product
 WHERE sale_price BETWEEN 100 AND 1000;

```

## IS NULL ,IS NOT NULL 判断是否为 NULL

- 要是空值

```bash
SELECT product_name, purchase_price
 FROM Product
 WHERE purchase_price IS NULL;
```

- 要不是空值

```bash

SELECT product_name, purchase_price
 FROM Product
 WHERE purchase_price IS NOT NULL;

```

## IN, NOT IN

但需要注意的是，在使用 IN 和 NOT IN 时是无法选取出 NULL 数据的。
实际结果也是如此，上述两组结果中都不包含进货单价为 NULL 的叉子和圆
珠笔。NULL 终究还是需要使用 IS NULL 和 IS NOT NULL 来进行判断

### IN 它不是区间 而是固定的值

```bash
SELECT product_name, purchase_price
 FROM Product
 WHERE purchase_price IN (320, 500, 5000);
```

等价于

```bash
SELECT product_name, purchase_price
 FROM Product
 WHERE purchase_price = 320
 OR purchase_price = 500
 OR purchase_price = 5000;
```

### NOT IN 不在这里面

```bash
SELECT product_name, purchase_price
 FROM Product
 WHERE purchase_price NOT IN (320, 500, 5000);
```

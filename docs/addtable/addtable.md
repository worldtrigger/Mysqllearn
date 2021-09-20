# 表的加减法

## 学习重点

```bash

● 集合运算就是对满足同一规则的记录进行的加减等四则运算。
● 使用UNION（并集）、INTERSECT（交集）、EXCEPT（差集）等集合运
算符来进行集合运算。
● 集合运算符可以去除重复行。
● 如果希望集合运算符保留重复行，就需要使用ALL选项。

```

## 注意事项

### 作为运算对象的列数必须相同

> 要是一部分包含 2 列,另外一部分包含 3 列则会发生错误,无法进行加法运算

```bash
-- 列数不一致时会发生错误
SELECT product_id, product_name
 FROM Product
UNION
SELECT product_id, product_name, sale_price
 FROM Product2;
```

### 作为运算对象的记录中的类型必须一致

> 像下面一个是数字,一个日期虽然列数相同但是数据类型不一致

```bash

-- 数据类型不一致时会发生错误
SELECT product_id, sale_price
 FROM Product
UNION
SELECT product_id, regist_date
 FROM Product2;

```

### 可以使用任何 SELECT 语句,但是 ORDER BY 子句只能在最后使用一次

通过 UNION 进行并集运算时可以使用任何形式的 SELECT 语句，
之前学过的 WHERE、GROUP BY、HAVING 等子句都可以使用。但是
ORDER BY 只能在最后使用一次

```bash

SELECT product_id, product_name FROM Product
 WHERE product_type = '厨房用具'
UNION
SELECT product_id, product_name
 FROM Product2
 WHERE product_type = '厨房用具'
ORDER BY product_id;

```

## 表的加法 UNION

> UNION(并集) 删除掉重复的数据,求并集

```bash

SELECT product_id, product_name FROM Product
 WHERE product_type = '厨房用具'
UNION
SELECT product_id, product_name
 FROM Product2
 WHERE product_type = '厨房用具'
ORDER BY product_id;

```

## 保留重复行 UNION ALL

- 这样的结果就是保留重复行

```bash

SELECT product_id, product_name
 FROM Product
UNION ALL
SELECT product_id, product_name
 FROM Product2;


```

# 对表进行分组

## 学习重点

- 使用 GRIUP BY 子句可以像切蛋糕那样将表分割,通过使用聚合函数和 GROUP BY 子句,可以依据商品种类或者登记日期等将表分割后再汇总

- 聚合键包含 NULL 时,在结果中会以"不确定行"(空行)的形式表现出来

- 使用聚合函数和 GROUP BY 子句需要注意以下 4 点

  1. 只能写在 SELECT 子句中
  2. GROUP BY 子句中不能使用 SELECT 子句列的别名
  3. GROUP BY 子句的结果是无序的
  4. WHERE 子句中不能使用聚合函数

## GROUP BY 子句

### 语法结构

```bash

SELECT <列名1>,<列名2>,<列名3> ... FROM <表名> GROUP BY <列名1>,<列名2>

```

- 举例

```bash

SELECT product_type,COUNT(*) FROM product GROUP BY product_type;

```

未使用 GROUP BY 是将表中的所有数据作为一组来对待,结果只有 1 行。
而使用 GROUP BY 会将表中的数据分为多个组进行处理,结果因分组而定。

在 GROUP BY 子句中指定的列称为`聚合列`或者`分组列`。由于能够决定表的切分方式,所以是非常重要的列,当然 GROUP BY 子句和 SELECT 子句一样,也可以通过`逗号`分隔指定多列

### 书写顺序

GROUP BY 的书写有严格的要求,一定要写在 FROM 子句之后(如果有 WHERE 子句的话需要写在 WHERE 子句之后),在定顺序如下

```bash

1.SELECT--->2.FROM------->3.WHERE------->4.GROUP BY

```

### 聚合键包含 NULL 的情况

当你利用 GROUP BY 把表分组,里面会有 NULL 的情况

```bash

SELECT purchase_price, COUNT(*)
 FROM Product
 GROUP BY purchase_price;

```

- 结果

```bash

purchase_price | count
----------------+-------
     | 2
 320 | 1
 500 | 1
 5000 | 1
 2800 | 2
 790 | 1

```

这个时候可以看出当聚合键包含 NULL 的时候,也会将 NULL 作为一组特定的数据

> 当聚合键中包含 NULL 的时候,在结果中会以'不确定'行(空行)的形式表现出来

### 使用 WHERE 子句时 GROUP BY 的执行结果

- 语法规则

```bash

SELECT <列名1>, <列名2>, <列名3>, ……
 FROM <表名>
 WHERE
 GROUP BY <列名1>, <列名2>, <列名3>, ……;

```

- 例句

```bash

SELECT purchase_price, COUNT(*)
 FROM Product
 WHERE product_type = '衣服'
 GROUP BY purchase_price;

```

- 语句最后的执行顺序

```bash

FROM---> WHERE ----> GROUP BY ---->SELECT

```

### 特别注意

- 不能出现聚合键以外的列

`使用GROUP BY 子句的时候,SELECT子句中不能出现聚合键之外的列`

举个例子

```bash

SELECT product_name, purchase_price, COUNT(*)
 FROM Product
 GROUP BY purchase_price;

```

你通过 price 把表分组了。加入 price 200 是一个组,那么你这里你会发现,雨衣，牙膏，牙刷的价格都是 200，这个时候就会报错了。因为不是一一对应了

- 不能使用别名

`使用GROUP BY 子句的时候,GROUP BY里面不允许使用列的别名`

举个例子

```bash

SELECT product_type AS pt, COUNT(*)
 FROM Product
 GROUP BY pt;

```

这样是不允许的。因为不会识别

- GROUP BY 的结果是无序的

`使用GROUP BY 获取的结果是随机的。无序的.所以不能排序`

- 禁止在 WHERE 子句中使用聚合函数

```bash

SELECT product_type, COUNT(*)
 FROM Product
 WHERE COUNT(*) = 2
 GROUP BY product_type;

```

上面的写法是错误的。不会执行

> 只有 SELECT 子句和 HAVING 子句（以及 ORDER BY 子句）中能够使用聚合函数。

### 多列分组

要是多列分组可以理解为两个列合并在一起例如

| 部门编号 | 部门名称 |
| -------- | -------- |
| N1       | 开发部门 |
| N2       | 测试部门 |

这样要是 GROUP BY 按照两个列来分组 实际查询的是

N1 开发部门 和 N2 测试部门

```bash
SELECT product_name, purchase_price, COUNT(*)
 FROM Product
 GROUP BY purchase_price,product_name;
```

### 使用场景

一般情况 GROUP BY 和聚合函数一起使用

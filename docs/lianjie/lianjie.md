# 连结查询

### 学习重点

```bash

● 联结（JOIN）就是将其他表中的列添加过来，进行“添加列”的集合运算。
UNION是以行（纵向）为单位进行操作，而联结则是以列（横向）为单位
进行的。
● 联结大体上分为内联结和外联结两种。首先请大家牢牢掌握这两种联结的
使用方法。
● 请大家一定要使用标准 SQL的语法格式来写联结运算，对于那些过时的
或者特定 SQL中的写法，了解一下即可，不建议使用

```

`以A中的列作为桥梁，将 B中满足同样条件的列汇集到同一结果之中`

### 内连接

- INNER JOIN (INNER 可以省略)

```bash

SELECT SP.shop_id, SP.shop_name, SP.product_id, P.product_name,
P.sale_price
 FROM ShopProduct AS SP INNER JOIN Product AS P ①
 ON SP.product_id = P.product_id;

```

- 注意点

> 1. 进行连接的时候需要在 FROM 子句中使用多张表
> 2. ON 子句 ON 后面接的是连接条件
> 3. SELECT 子句指定的列。

- 内连接和 WHERE 子句结合使用

```bash

SELECT SP.shop_id, SP.shop_name, SP.product_id, P.product_name,
P.sale_price
 FROM ShopProduct AS SP INNER JOIN Product AS P ①
 ON SP.product_id = P.product_id
 WHERE SP.shop_id = '000A';

```

### 外连接

- 语法结构和内连接一样

- 注意事项

```bash

外联的主表的关键字不一样结果也不一样。LEFT RIGHT,使用LEFT的时候写在左侧的表就是主表,使用RIGHT的时候写在右侧的表就是主表,不过使用二者的结果完全相同

```

- 实例化 (OUTER 可以省略)

```bash

SELECT SP.shop_id, SP.shop_name, SP.product_id, P.product_name,
P.sale_price
 FROM Product AS P LEFT OUTER JOIN ShopProduct AS SP ①
 ON SP.product_id = P.product_id;


```

### 一般情况都是两张表连接,也不排除三张表

```bash

SELECT SP.shop_id, SP.shop_name, SP.product_id, P.product_name, P.sale_price, IP.inventory_quantity
 FROM ShopProduct AS SP INNER JOIN Product AS P ①
 ON SP.product_id = P.product_id
 INNER JOIN InventoryProduct AS IP
 ON SP.product_id = IP.product_id
 WHERE IP.inventory_id = 'P001';

```

### 内连接和外连接的区别

内链接 A 表与 B 表链接 凡是 A 表和 B 表能够匹配上的记录查询出来(A,B 两表没有主付之分)

外连接 A 表与 B 表链接 AB 两张表 有一张是主表 有一张表是副表。主要查询主表，附带查询副表。当副表中的数据没有和主表匹配上，副表自动匹配 null 来填充

### 当不设定任何查询条件

- 那就会出现笛卡尔积

```bash
笛卡尔积 A表的行数xB表的行数  当两张表联合查询 没有任何限制。最后的结果是两张表的乘积
```

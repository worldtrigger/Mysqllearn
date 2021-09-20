# 聚合和排序

## 对表进行聚合查询

### 学习重点

- 使用聚合函数对表中的列进行计算`合计值`或者`平均值`等的汇总操作

- 通常聚合函数会对 NULL 以外的对象进行汇总,但是只有 COUNT 函数例外,使用 COUNT(\*)可以查询出包含 NULL 在内的全部数据的行数

- 使用 DISTINCT 关键字删除重复值

- 聚合函数只能用在 SELECT , HAVING,ORDER BY

### 聚合函数

通过 SQL 对数据的某种操作需要使用函数,计算表中全部数据的行数的时候,可以使用 COUNT 函数

### 5 个常用的聚合函数

COUNT 计算表中的记录数(行数)

SUM: 计算表中的数据的合计值

AVG: 计算表中的数据的平均值

MAX: 计算表中的数据的最大值

MIN: 计算表中的数据的最小值

`作用就是把表中的数据最后合并成一行`

`COUNT(*) 会包含NULL的行,其他聚合函数会排除NULL的行`

### COUNT 计算表中所有的行数

- 统计所有行的包括 NULL 的

```bash

SELECT COUNT(*) FROM product ;

```

这样的结果就是获取到所有行

- 统计所有行的不包括 NULL 的

```bash

SELECT COUNT(price) FROM product;

```

> COUNT 函数的结果可以根据参数的不同而不通。COUNT(\*)会得到包含 NULL 的数据行数,而 COUNT(<列名>)会得到 NULL 之外的数据行数

### 计算合计值

- SUM 函数 (求和运算)

> 里面必须写列名,他会自动删除值为 NULL 的行,不做求和计算

```bash

SELECT SUM(price) FROM product;

```

这样就做了求和运算

### 计算平均值

- AVG 求平均数

> 里面必须写列名,他会自动删除值为 NULL 的行,不做求平均数的计算

```bash
SELECT AVG(price) FROM product;
```

### 计算最大值和最小值

- MAX 和 MIN

> MAX 和 MIN 适用于任何列,也就是字符串类型的数据也能使用 MAX 和 MIN

```bash
SELECT MAX(regist_date), MIN(regist_date)
 FROM Product;
```

> MAX/MIN 函数几乎适用于所有数据类型的列。SUM/AVG 函数只适用于数值类型的列。

### 使用聚合函数删除重复值(DISTINCT)

- 删除重复的 type 类型

```bash

SELECT COUNT(DISTINCT product_type) FROM Product;

```

> 请注意 DISTINCT 必须写在括号内,因为要在计算之前就删除到重复的数据

- 不仅仅适用 COUNT,还能适用于 SUM,AVG 等等

```bash
SELECT SUM(sale_price), SUM(DISTINCT sale_price)
 FROM Product;
```

- DISTINCT 只能出现在所有字段的最前面

```bash
SELECT DISTINCT depto,job from emp ;
```

他表示 去掉所有 depto 和 job 联合起来 去掉重复的

> 在聚合函数的参数中使用 DISTINCT，可以删除重复数据。

### 也可以用在删除重复的数据

- IFNULL

聚合函数会排除 NULL，但有的时候字符串里面有 NULL 我们需要排除

```bash
SELECT IFNULL(NULL,'IFNULL function'); -- returns IFNULL function
```

DISTINCT 和 GROUP BY 都能删除重复的数据

```bash

SELECT DISTINCT product_type
 FROM Product;

SELECT product_type
 FROM Product
 GROUP BY product_type;

```

结果没有区别，但本质有区别

```bash

但其实这个问题本身就是本末倒置的，我们应该考虑的是该 SELECT 语句是否
满足需求。选择的标准其实非常简单，在“想要删除选择结果中的重复记录”时
使用 DISTINCT，在“想要计算汇总结果”时使用 GROUP BY。

```

# 为聚合结果指定条件

## 学习重点

- 使用 COUNT 函数等对表中数据进行汇总操作的时候,为其指定条件的不是 WHERE 子句二十 HAVING 子句

- 聚合函数可以在 SELECT 子句 HAVING 子句和 ORDER BY 子句中使用

- HAVING 子句要写在 GROUP BY 子句之后

- WHERE 子句用来进行数据行的条件,而 HAVING 用来针对分组的条件

## Having 子句

- 有的时候我们利用 GROUP BY 分组后,还需要在此基础上在限定条件比如 数据行数为 2 或者平均值为 500 等等

### 语法结构

```bash

SELECT <列名1>,<列名2>...FROM <表名> GROUP BY <列名1>,<列名2> HAVING <分组结果对应的条件>

```

HAVING 子句必须写在 GROUP BY 子句之后,其在 DBMS 内部的执行顺序也在 GROUP BY 之后

```bash

SELECT ---> FROM -----> WHERE---> GROUP BY ---> HAVING

```

- 举例

```bash

SELECT product_type, COUNT(*)
 FROM Product
 GROUP BY product_type
HAVING COUNT(*) = 2;

```

- 再比如

```bash

SELECT product_type, AVG(sale_price)
 FROM Product
 GROUP BY product_type
HAVING AVG(sale_price) >= 2500;

```

### HAVING 子句的构成要素

- 常数

- 聚合函数

- GROUP BY 子句中指定的列名(即聚合键)

> 在思考 HAVING 子句的使用方法时，把一次汇总后的结果（类似表 3-2 的表）作为 HAVING 子句起始点的话更容易理解。

### 相对于 HAVING 子句,更适合写在 WHERE 子句中的条件

WHERE 子句 = 指定行所对应的条件

HAVING 子句 = 指定组所对应的条件

通常情况下，为了得到相同的结果，将条件写在 WHERE 子句中要比写在 HAVING 子句中的处理速度更快，返回结果所需的时间更短。

# 视图

- 从 SQL 的角度来看,视图和表是相同的,两者的区别就在于表中保存的是实际的数据,而视图保存的是 SELECT 语句

- 使用视图,可以轻松完成跨多表查询数据等复杂操作

- 可以将常用的 SELECT 语句作为视图使用

- 创建视图需要使用 CREATE VIEW 语句

- 视图包含'不能使用 ORDER BY' 和 对 '其进行有限制的更新'两项限制

- 删除视图需要使用 DROP VIEW 语句

## 视图的优点

- 视图无需保存数据.表中存储的是实际数据,而视图中保存的是表中取出数据所使用的 SELECT 语句

- 可以将频繁使用的 SELECT 语句保存成视图,这样就不用每次都书写了。

## 创建视图的方法

### 语法结构

```bash

CREATE VIEW 视图名称(<视图列名1>,<视图列名2>,...) AS <SELECT语句>

```

- 备注

```bash

SELECT 语句需要书写在 AS 关键字之后。SELECT 语句中列的排列
顺序和视图中列的排列顺序相同，SELECT 语句中的第 1 列就是视图中的
第 1 列，SELECT 语句中的第 2 列就是视图中的第 2 列，以此类推。视图
的列名在视图名称之后的列表中定义

```

### 实例化

- 创建视图

```bash

CREATE VIEW ProductSum (product_type, cnt_product) AS
SELECT product_type, COUNT(*)
 FROM Product
 GROUP BY product_type;

```

- 使用视图

```bash

SELECT product_type, cnt_product
 FROM ProductSum;

```

### 注意

视图也支持多重视图,但是尽量不要使用多重视图,这样会降低性能

```bash

应避免在视图的基础上创建视图

```

## 视图的限制

### 定义视图的时候不能使用 ORDER BY 子句

```bash

CREATE VIEW ProductSum (product_type, cnt_product)
AS
SELECT product_type, COUNT(*)
 FROM Product
 GROUP BY product_type
ORDER BY product_type;

```

为什么不能使用 ORDER BY ? 因为视图和表一样,`数据行都是没有顺序的`

`特别注意的就是定义视图时不要使用ORDER BY`

### 对视图更新

不要对视图更新。因为视图是基于表。

(两张表)视图更新而表没更新。数据不一致了

(一张表)更新视图表里的数据也变化

```bash

(两张表)视图和表需要同时进行更新,因此通过汇总得到的视图无法更新
(一张表)视图变化那么表里的数据也变化

```

## 删除视图

### 删除视图

```bash

DROP VIEW 视图名称;

```

```bash

DROP VIEW 视图名称(<视图列名1>,<视图列名2>,...);

```

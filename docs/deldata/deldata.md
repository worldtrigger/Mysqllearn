# 数据的删除(DELETE 方法)

- DROP TABLE 可以将表完全删除

- DELETE 语句会留下表,而删除表中的全部数据

- TRUNCATE <表名>

## 删除整个表

```bash

DROP TABLE <表名>;

```

## DELETE 语句的基本用法

### 保留数据表

```bash

DELETE FROM <表名>;

```

> DELETE 语句的删除对象并不是表或者列，而是记录（行）。

### 指定删除对象的 DELETE 语句

```bash

DELETE FROM <表名> WHERE <条件>;

```

- 例子

```bash

DELETE FROM Product WHERE sale_price >= 4000;

```

> 特别注意删除的时候必须指定条件

```bash

可以通过WHERE子句指定对象条件来删除部分数据。

```

## TRUNCATE

也是删除表中的全部数据,保留表

但是不同的是 TRUNCATE 不能加条件。必须整张表

而且 TRUNCATE 的速度要比 DELETE 的速度快了很多

```bash

TRUNCATE <表名>;

```

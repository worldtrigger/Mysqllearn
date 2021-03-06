# 数据的更新

## UPDATE 基础语法

- 语法

```bash

UPDATE <表名> SET <列名> = <表达式>;

```

- 例子

```bash

UPDATE Product SET regist_date = '2009-10-10';

```

> 这种语句这样写很危险，他会把全表的那个列都修改成一个值

`所以使用UPDATE 后面必须接WHERE`

## 指定条件的 UPDATE 语句

- 语法

```bash

UPDATE <表名> SET <列名> = <表达式>,<列名2> =<表达式> WHERE <条件>;

```

## 多列更新

- 语法

```bash

UPDATE Product
 SET sale_price = sale_price * 10,
 purchase_price = purchase_price / 2
 WHERE product_type = '厨房用具';

```

## 当更新的时候条件是筛选出来的

- 语法

```bash
UPDATE `表名` AS table1
INNER JOIN
(SELECT * FROM `表名` WHERE `column` = value) AS table2
SET table1.xxx = value
WHERE table1.xxxx = table2.xxxx
```

- 实例

```bash

UPDATE emp AS RESULT
INNER JOIN
(
SELECT TIMESTAMPDIFF(YEAR,HIREDATE,now()) AS TIME,DEPTNO,ENAME,SAL*1.1 AS JIAGE FROM emp  WHERE TIMESTAMPDIFF(YEAR,HIREDATE,now()) >= 40 AND ENAME='SMITH'
)AS P1
SET RESULT.SAL = P1.JIAGE
WHERE
RESULT.ENAME = P1.ENAME

```

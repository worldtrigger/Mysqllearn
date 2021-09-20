# 函数

## 学习重点

- 根据用途 函数可以大致分为 算术函数,字符串函数,日期函数,转换函数和聚合函数

- 函数的种类很多。无需全部记住。只要记住代表性的即可

## 算术函数

### ABS 绝对值

- 语法结构

```bash

SELECT ABS(price) FROM product

```

你会发现当 ABS 的函数参数为 NULL 的时候,结果也是 NULL

### MOD 求余

```bash

MOD(被除数,除数)

```

MOD 是求余数的函数.例如 7/3 的余数是 1 因此 MOD(7,3)的结果也是 1,只能对整形列使用 MOD 函数

```bash

SELECT MOD(7,3) AS yushu FROM product;

```

### ROUND 四舍五入

- ROUND(对象数值,保留小数的位数)

```bash

SELECT ROUND(m,2) from product;

```

如果指定四舍五入的位数为 1，那么就会对小数点第 2 位进行四舍五入处
理。如果指定位数为 2，那么就会对第 3 位进行四舍五入处理

## 字符串函数

### 字符串拼接 CONCAT

```bash

SELECT str1,str2,CONCAT(str1,str2) AS result from product;

```

如果其中包含 NULL,那么得到结果也是 NULL

### 字符串长度

- LENGTH 中文占两个字节

```bash

LENGTH(字符串)

```

- 语法

```bash

SELECT str1, LENGTH(str1) AS len_str FROM product;

```

### 小写转换

- LOWER

```bash

LOWER(字符串)

```

- 语法结果

```bash

SELECT LOWER(str1) from product;

```

### UPPER 大写转换

```bash

UPPER(字符串)

```

- 实例化

```bash

SELECT str1,
 UPPER(str1) AS up_str
 FROM SampleStr

```

### REPLACE 字符串的替换

- REPLACE

```bash

REPLACE(对象字符串,替换前的字符串,替换后的字符串)

```

- 语法

```bash

SELECT str1, str2, str3,
 REPLACE(str1, str2, str3) AS rep_str
 FROM SampleStr;

```

### substring 函数

```bash

SUBSTRING（对象字符串 FROM 截取的起始位置 FOR 截取的字符数）

```

- 实例

```bash

SELECT str1,
 SUBSTRING(str1 FROM 3 FOR 2) AS sub_str
 FROM SampleStr;

```

## 日期函数

### CURRENT_DATE 当前日期

```bash

SELECT CURRENT_DATE;

```

如果在
2009 年 12 月 13 日执行该函数，会得到返回值“2009-12-13”。如果在
2010 年 1 月 1 日执行，就会得到返回值“2010-01-01”

### EXTRACT 截取日期元素

```bash

EXTRACT(日期元素 FROM 日期)

```

使用 EXTRACT 函数可以截取出日期数据中的一部分，例如“年”
“月”，或者“小时”“秒”等（代码清单 6-16）。该函数的返回值并不是日
期类型而是数值类型

- 实例化

```bash

SELECT CURRENT_TIMESTAMP,
 EXTRACT(YEAR FROM CURRENT_TIMESTAMP) AS year,
 EXTRACT(MONTH FROM CURRENT_TIMESTAMP) AS month,
 EXTRACT(DAY FROM CURRENT_TIMESTAMP) AS day,
 EXTRACT(HOUR FROM CURRENT_TIMESTAMP) AS hour,
 EXTRACT(MINUTE FROM CURRENT_TIMESTAMP) AS minute,
 EXTRACT(SECOND FROM CURRENT_TIMESTAMP) AS second;


```

## 转换函数

### CAST 改变类型

- 转换函数

```bash

CAST(转换前的值 AS 想要转换的数据类型)

```

- 实例化

```bash

SELECT CAST('0001' AS SIGNED INTEGER) AS int_col;
```

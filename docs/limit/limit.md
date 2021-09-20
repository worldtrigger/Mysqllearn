# 限制返回条数

- limit 级别最低

- limit 从 0 开始

- 两个参数 第一个是 startIndex ,第二个是 显示的 length

## 限制条数

- 返回 5 条数据,从第一条数据开始的数据

```bash

SELECT * FROM product order by id limit 0,5

```

- 返回第 2 条到第 7 条数据

```bash

SELECT * FROM product order by id limit 1,6

```

# Mysql 触发器

触发器是与表有关的数据库对象,在满足定义条件的时候触发。并执行触发器中定义的语句集合。

> 触发器尽量少的使用，因为不管如何，它还是很消耗资源，如果使用的话要谨慎的使用，确定它是非常高效的：触发器是针对每一行的；对增删改非常频繁的表上切记不要使用触发器，因为它会非常消耗资源

## 创建触发器

```bash

CREATE TRIGGER trigger_name trigger_time trigger_event ON tb_name FOR EACH ROW trigger_stmt
trigger_name：触发器的名称
tirgger_time：触发时机，为BEFORE或者AFTER
trigger_event：触发事件，为INSERT、DELETE或者UPDATE
tb_name：表示建立触发器的表明，就是在哪张表上建立触发器
trigger_stmt：触发器的程序体，可以是一条SQL语句或者是用BEGIN和END包含的多条语句
所以可以说MySQL创建以下六种触发器：
BEFORE INSERT,BEFORE DELETE,BEFORE UPDATE
AFTER INSERT,AFTER DELETE,AFTER UPDATE

```

其中触发器名参数指要创建的触发器的名字
BEFORE 和 AFTER 参数指定了触发执行的时间,在事件之前或是之后
FOR EACH ROW 表示任何一条记录上的操作满足触发事件都会触发该触发器

```bash
CREATE TRIGGER 触发器名 BEFORE|AFTER 触发事件
ON 表名 FOR EACH ROW
BEGIN
    执行语句列表
END
```

其中，BEGIN 与 END 之间的执行语句列表参数表示需要执行的多个语句，不同语句用分号隔开

> tips：一般情况下，mysql 默认是以 ; 作为结束执行语句，与触发器中需要的分行起冲突
> 为解决此问题可用 DELIMITER，如：DELIMITER ||，可以将结束符号变成||
> 当触发器创建完成后，可以用 DELIMITER ;来将结束符号变成;

- 实例化

```bash
mysql> DELIMITER ||
mysql> CREATE TRIGGER demo BEFORE DELETE
    -> ON users FOR EACH ROW
    -> BEGIN
    -> INSERT INTO logs VALUES(NOW());
    -> INSERT INTO logs VALUES(NOW());
    -> END
    -> ||
Query OK, 0 rows affected (0.06 sec)

mysql> DELIMITER ;
```

上面的语句中，开头将结束符号定义为||，中间定义一个触发器，一旦有满足条件的删除操作

就会执行 BEGIN 和 END 中的语句，接着使用||结束

最后使用 DELIMITER ; 将结束符号还原

## 总结

```bash

触发器是基于行触发的，所以删除、新增或者修改操作可能都会激活触发器，所以不要编写过于复杂的触发器，也不要增加过得的触发器，这样会对数据的插入、修改或者删除带来比较严重的影响，同时也会带来可移植性差的后果，所以在设计触发器的时候一定要有所考虑。

触发器是一种特殊的存储过程，它在插入，删除或修改特定表中的数据时触发执行，它比数据库本身标准的功能有更精细和更复杂的数据控制能力。

```

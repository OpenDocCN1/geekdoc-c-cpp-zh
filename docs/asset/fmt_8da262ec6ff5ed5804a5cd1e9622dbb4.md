
```
Tree as planned.
/-SYM-A-(Products_Ordered_Before_09012000:1 flag=0039)
/-OBJ----
/-AGGR---
/-OBJ----
/-SYM-V-(I2.invenqty:2 flag=0001)
--JOIN---
/-OBJ----
/-OBJ----
/-SYM-V-(P.prodnum:1 flag=0001)
--SYM-V-(I.prodnum:5 flag=0001)
--SYM-V-(I.custnum:3 flag=0001)
\-SYM-V-(C.custnum:1 flag=0001)
/-JOIN---
/-OBJ----
/-SYM-V-(I.prodnum:6 flag=0001)
--SYM-V-(I.custnum:3 flag=0001)
\-SYM-V-(C.custnum:1 flag=0001)
/-JOIN---
/-SYM-V-(C.custnum:1 flag=0001)
/-OBJ----
/-SRC----
\-TABL[WORK].CUSTOMERS opt=''
--FROM---
/-SYM-V-(I.prodnum:6 flag=0001)
/-OBJ----
--SYM-V-(I.custnum:3 flag=0001)
\-SRC----
\-TABL[WORK].INVOICE opt=''
--empty-
\-CEQ----
/-SYM-V-(C.custnum:1)
\-SYM-V-(I.custnum:3)
--FROM---
/-OBJ----
/-SYM-V-(P.prodnum:1 flag=0001)
\-SRC----
\-TABL[WORK].PRODUCTS opt=''
--empty-
/-SYM-V-(I.prodnum:6)
\-CEQ----
\-SYM-V-(P.prodnum:1)
/-SYM-V-(I2.invenqty:2 flag=0001)
/-OBJ----
--SYM-V-(I2.prodnum:1 flag=0001)
\-SRC----
--TABL[WORK].INVENTORY opt=''
--NAME--(orddate:3)
\-CLT----
\-LITN(14854) DATE.
--empty-
/-SYM-V-(I.prodnum:6)
\-CEQ----
\-SYM-V-(I2.prodnum:1)
--empty-
--empty-
--empty-
--empty-
/-SYM-A-(Products_Ordered_Before_09012000:1 flag=0039)
/-ASGN----
\-SYM-G-(#TEMG001:2 stat=8,0 from invenqty(0,0))
/-OBJ----
--empty-
/-SYM-G-(#TEMG001:2 stat=8,0 from invenqty(0,0))
/-TLST----
/-SYM-S-(invenqty:3 ss=0220x)
\-SLST----
--SSEL----
```

# `INOBS=` 选项

`INOBS=` 选项通过限制 `PROC SQL` 处理的行数来减少查询执行时间。该选项最常用于故障排除或调试目的，在这些情况下只需要少量行而不是表源中的所有行。使用 `INOBS=` 选项控制输入时处理的行数与指定 SAS 系统选项 `OBS=` 类似。以下示例说明 `INOBS=` 选项限制为 `PRODUCTS` 表中的前 10 行。SAS 日志中还显示了一条警告消息，指出由于 `INOBS=` 选项，已读取的记录数限制为 10。

## SQL 代码

```
PROC SQL INOBS=10;
  SELECT *
    FROM PRODUCTS;
QUIT;
```

## SAS 日志结果

```
PROC SQL INOBS=10;
  SELECT *
    FROM PRODUCTS;
WARNING: Only 10 records were read from WORK.PRODUCTS due to INOBS=
option.
QUIT;
```

在下一个示例中，`INOBS=` 选项设置为 5，用于笛卡尔积连接（`WHERE` 子句缺失）。在没有 `WHERE` 子句的情况下指定 `INOBS=5` 的双向连接会将每个表中的行数限制为 5，从而产生最多 25 行。

## SQL 代码

```
PROC SQL INOBS=5;
  SELECT prodname, prodcost, manufacturers.manunum, manuname
    FROM PRODUCTS, MANUFACTURERS;
QUIT;
```

## SAS 日志结果

```
PROC SQL INOBS=5;
  SELECT prodname, prodcost, manufacturers.manunum, manuname
    FROM PRODUCTS, MANUFACTURERS;
NOTE: The execution of this query involves performing one or more
Cartesian product joins that cannot be optimized.
WARNING: Only 5 records were read from WORK.MANUFACTURERS due to
INOBS= option.
WARNING: Only 5 records were read from WORK.PRODUCTS due to
INOBS= option.
QUIT;
```

# `LOOPS=` 选项

`LOOPS=` 选项通过限制查询内部循环的处理次数来减少查询执行时间。与 `INOBS=` 和 `OUTOBS=` 选项一样，`LOOPS=` 选项用于故障排除或调试，以防止消耗过多的计算机资源或在处理多表连接时创建大型内部表。以下示例显示 `LOOPS=` 选项限制为通过 `PRODUCTS` 表中的行进行八次内部循环。

## SQL 代码

```
PROC SQL LOOPS=8;
    SELECT *
    FROM PRODUCTS;
QUIT;
```

## SAS 日志结果

```
PROC SQL LOOPS=8;
    SELECT *
    FROM PRODUCTS;
WARNING: PROC SQL statement interrupted by LOOPS=8 option.
QUIT;
```

## 结果

| 产品编号 | 产品名称 | 制造商编号 | 产品类型 | 产品成本 |

|---|---|---|---|---|

| 1110 | 梦想机器 | 111 | 工作站 | $3,200.00 |

| 1200 | 商用机器 | 120 | 工作站 | $3,300.00 |

| 1700 | 旅行笔记本电脑 | 170 | 笔记本电脑 | $3,400.00 |

下一个示例展示了在三表连接中应用 `LOOPS=` 选项时会发生什么，通过将处理的内层循环数限制为 50，以防止创建庞大且低效的内部表。要确定赋予 `LOOPS=` 选项的适当值，可以在 `%PUT` 语句中指定 `&SQLLOOPS` 宏变量。要了解有关此宏变量的更多信息，请参阅本章后面的“宏变量”一节。

## SQL 代码

```
PROC SQL LOOPS=50;
    SELECT P.prodname, P.prodcost,
        M.manuname,
        I.invqty
    FROM PRODUCTS  P,
        MANUFACTURERS  M,
        INVOICE  I
    WHERE P.manunum = M.manunum AND
        P.prodnum = I.prodnum AND
        M.manunum = 500;
QUIT;
```

## 结果

| 产品名称 | 产品成本 | 制造商名称 | 发票数量 - 已售单位 |

|---|---|---|---|

| 电子表格软件 | $299.00 | KPL Enterprises | 5 |

| 数据库软件 | $399.00 | KPL Enterprises | 2 |

# `RESET` 语句

`RESET` 语句用于添加、删除或更改一个或多个 `PROC SQL` 选项，而无需重新启动过程。一旦指定了某个选项，它将一直有效，直到被更改或重置。使用 `RESET` 语句更改选项是一种方便的调试技术。下面的示例演示了如何通过将 `FEEDBACK` 选项重置为 `NOFEEDBACK` 来关闭该选项。关闭此选项后，可以防止 `SELECT *`（通配符）语句展开为其所代表的列列表。

## SQL 代码

```
PROC SQL FEEDBACK;
    SELECT *
        FROM PRODUCTS;
RESET NOFEEDBACK;
    SELECT *
        FROM PRODUCTS
            WHERE PRODTYPE='Software';
QUIT;
```

## SAS 日志结果

```
SELECT *
    FROM PRODUCTS;
NOTE: Statement transforms to:
select PRODUCTS.prodnum, PRODUCTS.prodname, PRODUCTS.manunum,
    PRODUCTS.prodtype, PRODUCTS.prodcost
    from PRODUCTS;
RESET NOFEEDBACK;
SELECT *
    FROM PRODUCTS
        WHERE PRODTYPE='Software';
```

可以在一个 `RESET` 语句中重置多个选项。`PROC SQL` 和 `RESET` 语句中的选项可以按任意顺序指定。下一个示例演示了如何在一个 `RESET` 语句中，通过 `NODOUBLE` 选项将双倍行距输出更改为单倍行距输出，通过 `NONUMBER` 选项抑制行号，并通过 `OUTOBS=` 选项将输出行数更改为最大行数。

## SQL 代码

```
PROC SQL DOUBLE NUMBER OUTOBS=1;
  SELECT *
    FROM PRODUCTS
    WHERE PRODTYPE='Software';
RESET NODOUBLE NONUMBER OUTOBS=MAX;
  SELECT *
    FROM PRODUCTS
    WHERE PRODTYPE='Software';
QUIT;
```

## SAS 日志结果

```
PROC SQL DOUBLE NUMBER OUTOBS=1;
  SELECT *
    FROM PRODUCTS
    WHERE PRODTYPE='Software';
WARNING: Statement terminated early due to OUTOBS=1 option.
RESET NODOUBLE NONUMBER OUTOBS=MAX;
  SELECT *
    FROM PRODUCTS
    WHERE PRODTYPE='Software';
QUIT;
```

## 输出结果

| 行 | 产品编号 | 产品名称 | 制造商编号 | 产品类型 | 产品成本 |

| --- | --- | --- | --- | --- | --- |

| 1 | 5001 | 电子表格软件 | 500 | 软件 | $299.00 |

| 产品编号 | 产品名称 | 制造商编号 | 产品类型 | 产品成本 |

| --- | --- | --- | --- | --- |

| 5001 | 电子表格软件 | 500 | 软件 | $299.00 |

| 5002 | 数据库软件 | 500 | 软件 | $399.00 |

| 5003 | 文字处理软件 | 500 | 软件 | $299.00 |

| 5004 | 图形软件 | 500 | 软件 | $299.00 |

下一个示例展示了一个 `UPDATE` 查询，该查询使用 `UNDO_POLICY=REQUIRED`（默认值）选项来撤销在出错之前执行的所有更新。（注意：由于这是该选项的默认值，因此可以省略。）在第二个更新查询之前发出 `RESET UNDO_POLICY=NONE` 语句，以更改更新的处理方式。`NONE` 选项会保留所有已进行的更新，无论是否检测到错误。系统会显示一条警告消息，提醒您更新处理方式已发生更改。

## SQL 代码

```
PROC SQL UNDO_POLICY=REQUIRED;
    UPDATE PRODUCTS
        SET PRODCOST = PRODCOST - (PRODCOST * 0.2)
        WHERE UPCASE(PRODTYPE) = 'LAPTOP';
    RESET UNDO_POLICY=NONE;
    UPDATE PRODUCTS
        SET PRODCOST = PRODCOST - (PRODCOST * 0.2)
        WHERE UPCASE(PRODTYPE) = 'LAPTOP';
QUIT;
```

## SAS 日志结果

```
PROC SQL UNDO_POLICY=REQUIRED;
    UPDATE PRODUCTS
        SET PRODCOST = PRODCOST - (PRODCOST * 0.2)
        WHERE UPCASE(PRODTYPE) = 'LAPTOP';
NOTE: 1 row was updated in WORK.PRODUCTS.
RESET UNDO_POLICY=NONE;
    UPDATE PRODUCTS
        SET PRODCOST = PRODCOST - (PRODCOST * 0.2)
        WHERE UPCASE(PRODTYPE) = 'LAPTOP';
WARNING: The SQL option UNDO_POLICY=REQUIRED is not in effect. If an error is detected when processing this UPDATE statement, that error will not cause the entire statement to fail.
NOTE: 1 row was updated in WORK.PRODUCTS.
QUIT;
```

# `EXEC`/`NOEXEC` 选项

`NOEXEC` 选项检查 SQL 过程内所有非查询语句（如 `CREATE TABLE` 或 `ALTER TABLE`）是否存在与语法相关的错误，并在 SAS 日志中显示任何已识别的错误。`NOEXEC` 选项与 `VALIDATE` 语句类似，它检查语法正确性，而不执行任何输入数据。`NOEXEC` 选项与 `VALIDATE` 语句之间的唯一区别在于它们的指定方式。如前所述，`VALIDATE` 语句在每条 `SELECT` 语句之前指定；而 `NOEXEC`/`EXEC` 选项可以作为 `PROC SQL` 语句选项指定，也可以在 `RESET` 语句中指定。

为了说明故障排除和调试过程，将使用 `NOEXEC` 和 `EXEC` 选项展示以下非查询 SQL 代码。下一个示例说明，在检查语法正确性后，非查询 `CREATE TABLE` 语句不会被执行。由于指定了 `NOEXEC` 选项，任何与语法相关的错误都会自动显示在 SAS 日志中。

## SQL 代码

```
PROC SQL NOEXEC;
    CREATE TABLE SOFTWARE_PRODUCTS
        SELECT *
            FROM PRODUCTS
                WHERE PRODTYPE = 'Software';
```

如 SAS 日志所示，发现一个语法错误，并显示由此产生的错误。

## SAS 日志结果

```
PROC SQL NOEXEC;
    CREATE TABLE SOFTWARE_PRODUCTS
        SELECT *
        ------
            73
ERROR 73-322: Expecting an AS.
            FROM PRODUCTS
                WHERE PRODTYPE = 'Software';
```

在下一个示例中，在 `NOEXEC` 选项仍然有效的情况下，`CREATE TABLE` 语句中指定了 `AS` 关键字，从而纠正了上一个示例中显示的语法错误。

## SQL 代码

```
CREATE TABLE SOFTWARE_PRODUCTS AS
    SELECT *
        FROM PRODUCTS
            WHERE PRODTYPE = 'Software';
```

如 SAS 日志所示，未发现语法错误，但由于 `NOEXEC` 选项仍然有效，`CREATE TABLE` 语句未被执行。

## SAS 日志结果

```
PROC SQL NOEXEC;
    CREATE TABLE SOFTWARE_PRODUCTS AS
        SELECT *
            FROM PRODUCTS
                WHERE PRODTYPE = 'Software';
NOTE: Statement not executed due to NOEXEC option.
```

下一个示例演示了使用 `RESET` 语句将 `NOEXEC` 选项更改为 `EXEC`，从而使无错误的非查询代码得以执行。

## SQL 代码

```
RESET EXEC;
CREATE TABLE SOFTWARE_PRODUCTS  AS
    SELECT *
        FROM PRODUCTS
            WHERE PRODTYPE = 'Software';
QUIT;
```

如 SAS 日志所示，未发现语法错误。并且由于指定了 `RESET` 语句将 `NOEXEC` 选项更改为 `EXEC`，`CREATE TABLE` 语句得以执行。

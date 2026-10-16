

# SQL 代码

```
%MACRO DUPS(LIB, TABLE, GROUPBY);
    PROC SQL FEEDBACK;
        SELECT &GROUPBY, COUNT(*) AS Duplicate_Rows
            FROM &LIB..&TABLE
                GROUP BY &GROUPBY
                    HAVING COUNT(*) > 1;
    QUIT;
%MEND DUPS;
%DUPS(WORK,PRODUCTS,PRODTYPE);
```

# SAS 日志结果

```
%MACRO DUPS(LIB, TABLE, GROUPBY);
    PROC SQL FEEDBACK;
        SELECT &GROUPBY, COUNT(*) AS Duplicate_Rows
            FROM &LIB..&TABLE
                GROUP BY &GROUPBY
                    HAVING COUNT(*) > 1;
    QUIT;
%MEND DUPS;
%DUPS(WORK,PRODUCTS,PRODTYPE);
NOTE: Statement transforms to:
    select PRODUCTS.prodtype, COUNT(*) as Duplicate_Rows
        from WORK.PRODUCTS
            group by PRODUCTS.prodtype
                having COUNT(*)>1;
```

你也可以指定 %PUT 语句而不是 FEEDBACK 选项来在宏解析后显示宏变量的值。下一个示例说明在 QUIT 和 %MEND 语句之间插入宏语句 %PUT LIB = &LIB TABLE = &TABLE GROUPBY = &GROUPBY 以产生下面所示的结果。

# SQL 代码

```
%MACRO DUPS(LIB, TABLE, GROUPBY);
    PROC SQL;
        SELECT &GROUPBY, COUNT(*) AS Duplicate_Rows
            FROM &LIB..&TABLE
                GROUP BY &GROUPBY
                    HAVING COUNT(*) > 1;
    QUIT;
    %PUT LIB = &LIB TABLE = &TABLE GROUPBY = &GROUPBY;
%MEND DUPS;
%DUPS(WORK,PRODUCTS,PRODTYPE);
```

# SAS 日志结果

```
%MACRO DUPS(LIB, TABLE, GROUPBY);
... code not shown ...
LIB = WORK TABLE = PRODUCTS GROUPBY = PRODTYPE
```

# _METHOD 和 _TREE 选项配合 MSGLEVEL=I

作为故障排除和调试工具，PROC SQL 支持 _METHOD 和 _TREE 选项。这些选项对于分别理解 SQL 优化器选择的<|message|>处理方法层次结构以及查询计划的内部形式非常有用。为了帮助用户理解从 _METHOD 选项生成并在 SAS 日志中显示的具体代码，Table 9.4 中列出了代码表以及简要描述。

当与 _METHOD 和 _TREE 选项结合使用时，MSGLEVEL=I 系统选项会在 SAS 日志中显示与索引使用、合并处理和排序实用程序使用相关的额外消息。

# 表 9.4：从 _METHOD 选项生成并在 SAS 日志中显示的代码

| Code | Description |
|------|-------------|
| SQXCRTA | Create table as Select. |
| SQXSLCT | Select statement or clause. |
| SQXJSL | Step loop join (Cartesian). |
| SQXJM | Merge join operation. |
| SQXJNDX | Index join operation. |
| SQXJHSH | Hash join operation. |
| SQXSORT | Sort operation. |
| SQXSRC | Source rows from table. |
| SQXFIL | Rows filtration. |
| SQXSUMG | Summary stat (aggregates) with GROUP BY clause. |
| SQXSUMN | Summary stat with no GROUP BY clause. |

# SQL 代码

```
OPTIONS MSGLEVEL=I;
PROC SQL _METHOD _TREE;
SELECT sum(inventory.inventqty)
AS Products_Ordered_Before_09012000
FROM PRODUCTS P,
INVOICE I,
CUSTOMERS C,
INVENTORY I2
WHERE I2.orddate < mdy(09,01,00) AND
    P.prodnum = I.prodnum AND
    I.custnum = C.custnum AND
    I.prodnum = I2.prodnum;
QUIT;
```

# SAS 日志结果

```
OPTIONS MSGLEVEL=I;
PROC SQL _METHOD _TREE;
    SELECT sum(inventory.invenqty)
        AS Products_Ordered_Before_09012000
    FROM PRODUCTS    P,
        INVOICE      I,
        CUSTOMERS    C,
        INVENTORY    I2
    WHERE I2.orddate < mdy(09,01,00) AND
          P.prodnum  = I.prodnum AND
          I.custnum  = C.custnum AND
          I.prodnum  = I2.prodnum;

NOTE: SQL execution methods chosen are:
    sqxslct
        sqxsum
            sqxjhsh
                sqxjhsh
                    sqxjhsh
                        sqxsrc( WORK.CUSTOMERS(alias = C) )
                        sqxsrc( WORK.INVOICE(alias = I) )
                        sqxsrc( WORK.PRODUCTS(alias = P) )
                    sqxsrc( WORK.INVENTORY(alias = I2) )
```

_TREE 选项在指定时，提供查询优化器处理查询执行方式的图形表示。基本上，查询执行计划显示了优化器基于使用的语句、子句、选项、关键字和其他编码结构如何解释和执行查询。

当提交查询执行时，优化器确定执行查询的最优方式，从而构建执行计划。通常，基于成本的优化器选择什么执行计划的决定会受到估计的 CPU 和 IO 处理成本以及查询预计执行速度的影响。结果是一个查询执行计划，描绘了标签、节点、输入源、连接参数、where 子句条件和其他描述性信息的树形结构，如下所示。

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

# INOBS= 选项

INOBS= 选项通过限制 PROC SQL 处理的行数来减少查询执行时间。该选项最常用于故障排除或调试目的，在这些情况下只需要少量行而不是表源中的所有行。使用 INOBS= 选项控制输入时处理的行数与指定 SAS 系统选项 OBS= 类似。以下示例说明 INOBS= 选项限制为 PRODUCTS 表中的前 10 行。SAS 日志中还显示了一条警告消息，指出由于 INOBS= 选项，已读取的记录数限制为 10。

# SQL 代码

```
PROC SQL INOBS=10;
  SELECT *
    FROM PRODUCTS;
QUIT;
```

# SAS 日志结果

```
PROC SQL INOBS=10;
  SELECT *
    FROM PRODUCTS;
WARNING: Only 10 records were read from WORK.PRODUCTS due to INOBS=
option.
QUIT;
```

在下一个示例中，INOBS= 选项设置为 5，用于笛卡尔积连接（WHERE 子句缺失）。在没有 WHERE 子句的情况下指定 INOBS=5 的双向连接会将每个表中的行数限制为 5，从而产生最多 25 行。

# SQL 代码

```
PROC SQL INOBS=5;
  SELECT prodname, prodcost, manufacturers.manunum, manuname
    FROM PRODUCTS, MANUFACTURERS;
QUIT;
```

# SAS 日志结果

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

# LOOPS= 选项

LOOPS= 选项通过限制查询内部循环的处理次数来减少查询执行时间。与 INOBS= 和 OUTOBS= 选项一样，LOOPS= 选项用于故障排除或调试，以防止消耗过多的计算机资源或在处理多表连接时创建大型内部表。以下示例显示 LOOPS= 选项限制为通过 PRODUCTS 表中的行进行八次内部循环。


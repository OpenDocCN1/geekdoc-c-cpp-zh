
第二种方法使用PROC SQL访问字典表TABLES和COLUMNS，以判断表是否足够大，从而利用索引带来的性能改进。请参见下面的输出。

## SQL代码

```
PROC SQL;
    SELECT MEMNAME, NPAGE
        FROM DICTIONARY.TABLES
        WHERE LIBNAME='WORK' AND
            MEMNAME='INVENTORY';

    SELECT VARNUM, NAME, TYPE, LENGTH, FORMAT,
            INFORMAT, LABEL
        FROM DICTIONARY.COLUMNS
        WHERE LIBNAME='WORK' AND
            MEMNAME='INVENTORY';
QUIT;
```

## 结果

| 成员名称 | 页数 |
|---|---:|
| INVENTORY | 1 |

| 表中列序号 | 列名 | 列类型 | 列长度 | 列格式 | 列输入格式 | 列标签 |
|---:|---|---|---:|---|---|---|
| 1 | prodnum | num | 3 |  |  | 产品编号 |
| 2 | inventqty | num | 3 |  |  | 库存数量 |
| 3 | orddate | num | 4 | MMDDYY10. | MMDDYY10. | 最近一次订购库存日期 |
| 4 | invencst | num | 6 | DOLLAR10.2 |  | 库存成本 |
| 5 | manunum | num | 3 |  |  | 制造商编号 |

表10.2比较了顺序表访问与索引表访问。尽管性能提升取决于数据，但将索引应用于WHERE子句中一小部分数据时，能够实现最大的提升。

## 表10.2：顺序访问与索引访问对比

| 条件 | 顺序访问 | 索引 |
|---|---|---|
| 页数 < 3 页（根据CONTENTS输出） | 是 | 否 |
| 表较小 | 是 | 否 |
| 表频繁更新 | 是 | 否 |
| 基于WHERE处理的数据子集较大 | 是 | 否 |
| 表访问不频繁 | 是 | 否 |
| 内存和磁盘空间有限 | 是 | 否 |
| 数据子集较小（数据总量的1%–25%） | 否 | 是 |

系统消息会显示出来，提供有助于调整与任何数据集关联的索引的信息。将系统选项MSGLEVEL=设置为“I”，允许SAS显示与一个或多个索引的存在相关的关键信息（如果有），用于优化WHERE子句处理。启用MSGLEVEL=选项后，SAS日志显示，在WHERE子句处理的优化过程中选择了简单索引INVENQTY。

## SAS日志

```
PROC SQL;
    CREATE INDEX INVENQTY ON INVENTORY;
NOTE: Simple index invenqty has been defined.
NOTE: PROCEDURE SQL used:
      real time          0.04 seconds
    SELECT *
      FROM INVENTORY
      WHERE invenqty < 3;
INFO: Index invenqty selected for WHERE clause optimization.
    QUIT;
NOTE: PROCEDURE SQL used:
      real time          0.65 seconds
```

## 使用索引优化WHERE子句处理

为了从包含SQL过程代码的程序中获得尽可能好的性能，可以将索引和WHERE子句一起使用（请参见下面的列表）。使用WHERE子句将表处理限制为所选行的子集（更多信息，请参见第2章“使用PROC SQL处理数据”）。当索引存在时，SQL处理器会在WHERE子句处理过程中决定是否利用该索引。尽管SQL优化器会确定使用索引最终是否有利于性能，但当它使用索引时，处理速度可能会得到提升。

-   比较运算符，如 EQ (=)、LT (<)、GT (>)、LE (<=)、GE (>=) 和 NOT
-   与 IN 运算符一起使用的比较运算符
-   带有冒号修饰符的比较运算符（例如，NOT =:"Ab"）
-   CONTAINS 运算符
-   IS NULL 或 IS MISSING 运算符
-   模式匹配运算符，如 LIKE 和 NOT LIKE

## 构建高效逻辑条件

构建高效逻辑条件会直接影响处理成本。由于SQL优化器从左到右评估一系列AND表达式，因此WHERE子句中的AND条件链应首先指定限制性最强的表达式。这样指定，可以绕过不满足WHERE子句中第一个条件值的行，从而消耗更少的资源。例如，下面的SQL查询可能会消耗更多资源并运行更慢，因为即使产品成本超过99.00美元时，也首先要判断第一个条件“SOFTWARE”。

## SQL代码（效率较低）

```
PROC SQL;
    SELECT *
        FROM PRODUCTS
            WHERE UPCASE(PRODTYPE) = 'SOFTWARE' AND
                PRODCOST < 100.00;
QUIT;
```

对于这些数据，要在减少CPU资源的同时产生与前一示例相同的结果，一种更高效的方法是将最不可能出现的条件放在前面，如下所示。

## SQL代码（更高效）

```
PROC SQL;
    SELECT *
        FROM PRODUCTS
            WHERE PRODCOST < 100.00 AND
                UPCASE(PRODTYPE) = 'SOFTWARE';
QUIT;
```

另一种常见的构造是使用一系列OR条件相等性测试或IN谓词来选择匹配多个条件的行。程序员通常按数值大小或字母顺序指定这些列表，以便于阅读和/或维护。更好、更高效的方式是按出现频率从高到低的顺序构造常量列表。

## SAS日志结果

```
PROC SQL STIMER;
NOTE: SQL Statement used (Total process time):
    real time          0.00 seconds
    cpu time           0.01 seconds

SELECT *
    FROM PRODUCTS
    WHERE UPCASE(PRODTYPE) IN ('LAPTOP', 'SOFTWARE');
NOTE: SQL Statement used (Total process time):
    real time          0.08 seconds
    cpu time           0.04 seconds
```

一种在不改变结果的同时更高效处理相同数据的方法是，将条件“SOFTWARE”放在前面，如下所示：

## SQL代码（更高效）

```
PROC SQL STIMER;
SELECT *
    FROM PRODUCTS
    WHERE UPCASE(PRODTYPE) IN ('SOFTWARE', 'LAPTOP');
QUIT;
```

## SAS日志结果

```
PROC SQL STIMER;
SELECT *
    FROM PRODUCTS
    WHERE UPCASE(PRODTYPE) IN ('SOFTWARE', 'LAPTOP');
NOTE: SQL Statement used (Total process time):
    real time          0.02 seconds
    cpu time           0.03 seconds

QUIT;
```

## 避免使用UNION

UNION通过创建两个内部集合，然后将结果合并排序来执行。重复行会自动从最终结果中消除。两个集合的UNION的维恩图表示集合中所有不同的元素，如图10.1所示。

## 图10.1：维恩图

![](img/9d3e4d8fa063e50a0c9985e34cf9d6e8_384_0.png)

例如，表示UNION集合的SQL过程代码首先从每个查询构造两个结果集，将这两个结果集合并排序，然后从最终结果中消除重复行。

## SQL代码（效率较低）

```
OPTIONS FULLSTIMER;
PROC SQL;
    SELECT *
        FROM PRODUCTS
            WHERE UPCASE(PRODTYPE) = 'LAPTOP'

    UNION

    SELECT *
        FROM PRODUCTS
            WHERE UPCASE(PRODTYPE) = 'SOFTWARE';
QUIT;
```

## SAS日志结果

```
OPTIONS FULLSTIMER;
PROC SQL;
    SELECT *
        FROM PRODUCTS
            WHERE UPCASE(PRODTYPE) = 'LAPTOP'

    UNION

    SELECT *
        FROM PRODUCTS
            WHERE UPCASE(PRODTYPE) = 'SOFTWARE';
QUIT;
NOTE: PROCEDURE SQL used (Total process time):
    real time          0.16 seconds
    user cpu time      0.00 seconds
    system cpu time    0.04 seconds
    memory             634.09k
    OS Memory          6768.00k
    Timestamp          06/03/2012 04:59:57 PM
```

为了提高UNION性能，可以将SQL过程代码转换为在WHERE子句中使用OR条件的单一查询。下一个示例说明如何通过将UNION转换为在WHERE子句中使用OR运算符的单一查询，使前面的SQL过程代码更高效。

## SQL代码（高效）

```
OPTIONS FULLSTIMER;
PROC SQL;
    SELECT DISTINCT *
        FROM PRODUCTS
        WHERE UPCASE(PRODTYPE) = 'SOFTWARE' OR
              UPCASE(PRODTYPE) = 'LAPTOP';
QUIT;
```

## SAS日志结果

```
OPTIONS FULLSTIMER;
PROC SQL;
    SELECT DISTINCT *
        FROM PRODUCTS
        WHERE UPCASE(PRODTYPE) = 'SOFTWARE' OR
              UPCASE(PRODTYPE) = 'LAPTOP';
QUIT;
NOTE: PROCEDURE SQL used (Total process time):
    real time          0.10 seconds
    user cpu time      0.04 seconds
    system cpu time    0.01 seconds
    memory             565.60k
    OS Memory          6768.00k
    Timestamp          06/03/2012 05:06:55 PM
```

下一个示例说明如何通过将UNION转换为在WHERE子句中使用IN谓词的单一查询，使前面的SQL过程代码更高效。

## SQL代码（高效）

```
OPTIONS FULLSTIMER;
PROC SQL;
    SELECT DISTINCT *

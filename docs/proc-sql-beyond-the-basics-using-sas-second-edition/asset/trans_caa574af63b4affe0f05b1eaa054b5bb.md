

## SAS 日志结果

```
PROC SQL;
    CREATE VIEW NO_CAN_DO_VIEW AS
        SELECT *
            FROM NO_CAN_DO_VIEW;
NOTE: SQL view WORK.NO_CAN_DO_VIEW has been defined.
    SELECT *
        FROM NO_CAN_DO_VIEW;
ERROR: The SQL View WORK.NO_CAN_DO_VIEW is referenced recursively.
    QUIT;
NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE SQL used (Total process time):
        real time           0.00 seconds
        cpu time            0.01 seconds
```

## 视图与 SAS 过程

在大多数情况下（但并非所有情况），视图可以像输入 SAS 数据集一样用于所有可用的 SAS 过程。在第一个示例中，INVENTORY_VIEW 视图被用作 MEANS 过程的输入，为数值变量生成简单的单变量描述性统计。访问 INVENTORY_VIEW 视图与访问 INVENTORY 表不同，因为视图内部编译过的可执行语句会被处理，从而将底层表中的当前数据提供给视图本身。视图语句以及 MEANS 过程中的语句和选项决定了会生成哪些信息。

下一个示例使用 INVENTORY_VIEW 视图作为 MEANS 过程的输入，为数值变量生成简单的单变量描述性统计。访问 INVENTORY_VIEW 视图与访问 INVENTORY 表不同，因为视图会从底层表派生并提供当前数据给视图本身。视图语句以及 MEANS 过程中的语句和选项决定了会生成哪些信息。

## SAS 代码

```
PROC MEANS DATA=INVENTORY_VIEW;
    TITLE1 'Inventory Statistical Report';
    TITLE2 'Demonstration of a View used in PROC MEANS';
RUN;
```

## SAS 日志结果

```
PROC MEANS DATA=INVENTORY_VIEW;
TITLE1 'Inventory Statistical Report';
TITLE2 'Demonstration of a View used in PROC MEANS';
RUN;
NOTE: There were 7 observations read from the dataset WORK.INVENTORY.
NOTE: There were 7 observations read from the dataset WORK.INVENTORY_VIEW.
NOTE: PROCEDURE MEANS used:
real time          0.32 seconds
```

## 结果

## 库存统计报告
在 PROC MEANS 中使用视图的演示
MEANS 过程

| 变量 | 标签 | N | 均值 | 标准差 | 最小值 | 最大值 |
| prodnum | 产品编号 | 7 | 3974.43 | 1763.50 | 1110.00 | 5004.00 |
| invqty | 库存数量 | 7 | 10.0000000 | 7.5055535 | 2.0000000 | 20.0000000 |
| invcnst | 库存成本 | 7 | 11357.14 | 17866.72 | 900.0000000 | 45000.00 |
| AverageAmount |  | 7 | 917.1428571 | 1121.71 | 70.0000000 | 2800.00 |

下一个示例使用 INVENTORY_VIEW 视图作为 PRINT 过程的输入，生成底层基表中包含值的详细列表。

注意：值得一提的是，与所有过程一样，所有过程选项和语句都可通过视图使用。

## SAS 代码

```
PROC PRINT DATA=INVENTORY_VIEW N NOOBS UNIFORM;
TITLE1 'Inventory Detail Listing';
TITLE2 'Demonstration of a View used in PROC PRINT';
format AverageAmount dollar10.2;
RUN;
```

## SAS 日志结果

```
PROC PRINT DATA=INVENTORY_VIEW N NOOBS UNIFORM;
    TITLE1 'Inventory Detail Listing';
    TITLE2 'Demonstration of a View used in a Procedure';
    format AverageAmount dollar10.2;
RUN;
NOTE: There were 7 observations read from the dataset WORK.INVENTORY.
NOTE: There were 7 observations read from the dataset WORK.INVENTORY_VIEW.
NOTE: PROCEDURE PRINT used:
      real time          0.04 seconds
```

## 结果

库存详细列表
在 PROC PRINT 中使用视图的演示

| prodnum | invqty | invcnst | AverageAmount |
|---------|--------|---------|---------------|
| 1110    | 20       | $45,000.00 | $2,250.00 |
| 1700    | 10       | $28,000.00 | $2,800.00 |
| 5001    | 5        | $1,000.00  | $200.00 |
| 5002    | 3        | $900.00    | $300.00 |
| 5003    | 10       | $2,000.00  | $200.00 |
| 5004    | 20       | $1,400.00  | $70.00 |
| 5001    | 2        | $1,200.00  | $600.00 |
|         |          | N = 7     |               |

## 视图与 DATA 步

正如你已经看到的，视图可以像数据集一样用作 SAS 过程的输入。现在你将看到，视图也是一个多用途组件，可以在 DATA 步中使用。这为你提供了一种受控的方式，可以在自定义报表程序中使用视图访问数据表。下一个示例将 INVENTORY_VIEW 视图用作 DATA 步的输入，就像它是一个 SAS 基表一样。注意，KEEP= 数据集选项只从 INVENTORY_VIEW 视图中读取两个变量。

## SAS 代码

```
OPTIONS FORMCHAR="|----|+|----+=|-|\/<>'*";
DATA _NULL_;
    SET INVENTORY_VIEW (KEEP=PRODNUM AVERAGEAMOUNT);
    FILE PRINT HEADER=H1;
    PUT @10 PRODNUM
        @30 AVERAGEAMOUNT DOLLAR10.2;
RETURN;
H1: PUT @9 'Using a View in a DATA Step'
    /// @5 'Product Number'
    @26 'Average Amount';
RETURN;
RUN;
```

## SAS 日志结果

```
OPTIONS FORMCHAR="|----|+|----+=|-|\/<>'*";
DATA _NULL_;
    SET INVENTORY_VIEW (KEEP=PRODNUM AVERAGEAMOUNT);
    FILE PRINT HEADER=H1;
    PUT @10 PRODNUM
        @30 AVERAGEAMOUNT DOLLAR10.2;
RETURN;
H1: PUT @9 'Using a View in a DATA Step'
    /// @5 'Product Number'
    @26 'Average Amount';
RETURN;
RUN;
NOTE: 11 lines were written to file PRINT.
NOTE: There were 7 observations read from the dataset WORK.INVENTORY.
NOTE: There were 7 observations read from the dataset WORK.INVENTORY_VIEW.
NOTE: DATA statement used:
      real time          0.00 seconds
```

## 输出

在 DATA 步中使用视图

产品编号    平均金额
1110              $2,250.00
1700              $2,800.00
5001              $200.00
5002              $300.00
5003              $200.00
5004              $70.00
5001              $600.00

## 消除冗余

数据冗余通常发生在两个或更多用户希望以不同方式查看相同数据时。为了防止冗余，组织应创建并维护一个主数据库环境，而不是在用户群体中传播一个或多个数据子集。后一种方法创造的环境不仅对组织有问题，对其用户和客户也是如此。

视图提供了一种消除或至少减少数据冗余程度的方法。视图不是让相同数据以多种形式存在，而是为所有人创建一个虚拟且可共享的数据库环境。与访问和报告过时信息以及与表和程序变更控制相关的问题都将被消除。

## 限制数据访问——安全性

随着数据安全问题对全球组织越来越重要，视图在控制或限制对敏感信息的访问方面提供了强大的替代方案。视图与表一样，可以防止未经授权的用户访问敏感数据部分。这一点很重要，因为安全漏洞不仅对组织的数据资源构成巨大风险，也对客户构成巨大风险。

可以构建视图来显示与底层基表中物理存在的数据不同的数据视图。可以显示特定列，而隐藏其他列。这有助于防止工资、医疗或信用卡数据等敏感信息落入不当之手。或者，视图可以包含一个任意复杂度的 WHERE 子句，以限制一组用户可以看到的行，同时隐藏其他行。在下一个示例中，创建了一个名为 SOFTWARE_PRODUCTS_VIEW 的视图，它显示原始表中的所有列，但不包括产品成本（PRODCOST）列，并且仅从 PRODUCTS 表中限制除 "Software" 之外的所有行。

## SQL 代码

```
PROC SQL;
    CREATE VIEW SOFTWARE_PRODUCTS_VIEW AS
        SELECT prodnum, prodname, manunum, prodtype
            FROM PRODUCTS
                WHERE UPCASE(PRODTYPE) IN ('SOFTWARE');
QUIT;
```

## SAS 日志结果

```
PROC SQL;
CREATE VIEW SOFTWARE_PRODUCTS_VIEW AS
SELECT prodnum, prodname, manunum, prodtype
FROM PRODUCTS
WHERE UPCASE(PRODTYPE) IN ('SOFTWARE');
NOTE: SQL view WORK.SOFTWARE_PRODUCTS_VIEW has been defined.
QUIT;
NOTE: PROCEDURE SQL used:
real time            0.17 seconds
```

SOFTWARE_PRODUCTS_VIEW 视图的功能就像它是一个基表一样，尽管它不包含任何数据行。除产品成本（PRODCOST）列之外，所有其他列均继承自 PRODUCTS 表中选定的列。视图决定从底层表处理哪些列和行，并且可选地，引用该视图的 SELECT 查询可以在处理过程中提供附加条件。在下一个示例中，在 SELECT 查询中引用了 SOFTWARE_PRODUCTS_VIEW 视图，并按产品名称（PRODNAME）升序排列。

## SQL 代码

```
PROC SQL;
SELECT *
FROM SOFTWARE_PRODUCTS_VIEW
ORDER BY prodname;
QUIT;
```

## 结果

| 产品编号 | 产品名称 | 制造商编号 | 产品类型 |
|---|---|---|---|
| 5002 | 数据库软件 | 500 | 软件 |
| 5004 | 图形软件 | 500 | 软件 |
| 5001 | 电子表格软件 | 500 | 软件 |
| 5003 | 文字处理软件 | 500 | 软件 |

## 隐藏逻辑复杂性

因为复杂的逻辑结构（如多路表连接、子查询或难以理解的数据关系）可能超出你所在领域其他员工的技能范围，你可能希望构建或定制视图，以便其他人可以轻松访问信息。下一个示例展示了如何


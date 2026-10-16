
在处理包含相似信息的两个表时，可以使用 `EXCEPT` 操作符来确定新增和修改的行。`EXCEPT` 操作符用于识别第一个表（或查询）中的行，但不用于识别第二个表（或查询）中的行。它还唯一地标识从第一个表到第二个表已更改的行。列按其在 `SELECT` 语句中出现的顺序进行比较。

如果在 `SELECT` 语句中指定了通配符字符“`*`”，则假定两个表在结构上彼此相同。让我们看一个例子。

假设你有 `CUSTOMERS` 文件的主表和备份表，并且想要比较它们以识别新增和更改的行。`EXCEPT` 操作符如下一个示例所示返回 `CUSTOMERS` 表中所有新增或更改的行，这些行在 `CUSTOMERS_BACKUP` 表中不存在。如结果所示，有三行新客户被添加到 `CUSTOMERS` 表中，这些行之前在 `CUSTOMERS_BACKUP` 表中不存在。

### SQL 代码

```sql
PROC SQL;
    SELECT *
        FROM CUSTOMERS_BACKUP
    EXCEPT
    SELECT *
        FROM CUSTOMERS;
QUIT;
```

1 `EXCEPT` 操作符比较两个表中的行以识别存在于第一个表但不存在于第二个表中的行。

### 结果

| 客户编号 | 客户名称 | 客户所在城市 |

| 1302 | Software Intelligence Cor | Spring Valley |

| 1901 | Shipp Consulting | San Pedro |

| 1902 | Gupta Programming | Simi Valley |

## 复杂查询应用

查询应用形式多样，通常可分为三类：

- **面向生产的查询**很少更改，按需运行（例如，每天、每周、每月等），并由 `SQL` 语句、参数列表和/或操作查询组成。

- **临时查询**通常按需构建，通常只使用一次或以某种不可预测的方式使用，以解决特定需求或问题。

- **自定义查询**被归类为介于面向生产和临时查询之间，其中查询每次运行时基本相同，但存在条件、参数、操作处理（例如，创建新表、更新一个或多个表中的行、删除一个或多个表中的行，以及向现有表追加一个或多个行）和数据差异，必须进行处理。

在本节中，介绍了一些复杂的查询应用，以展示如何使用 `SQL` 过程来满足特定的处理和/或数据管理要求。这些应用部分基于许多 `SAS` 用户的需求、将流行的 `DATA` 步技术模拟为 `SQL` 查询，以及分享有趣的 `SQL` 过程编码技术和方法。

## 一对一、一对多、多对一和多对多关系

输入表通常根据一个表中的行与另一个表中的一个或多个行的关系来表征。此过程称为两个或多个表之间的数据关系，分为四类：

- 一对一

- 一对多

- 多对一

- 多对多

为了更好地理解如何处理数据源以产生理想的结果，能够区分四类数据关系是有帮助的。以下示例说明了在 `SQL` 过程中应用一对一、一对多、多对一和多对多数据关系的编码约定。

### SQL 代码

```sas
/* *************************************************************************/
/** PROGRAM NAME: DATA-RELATIONSHIPS.SAS                                 **/
/** PURPOSE..... : Derive one-to-one, one-to-many, many-to-one,          **/
/**               and many-to-many data relationships using              **/
/**               complex queries.                                        **/
/** AUTHOR...... : Kirk Paul Lafler                                       **/
/** DATE WRITTEN: August 30, 2012                                         **/
/***********************************************************************/
proc sql noprint;
/***********************************************************************/
/** ROUTINE..... : ONE-TO-ONE                                            **/
/** PURPOSE..... : Produce a one-to-one data relationship using          **/
/**               a base table with a unique key and a lookup             **/
/**               table with a unique key in an EQUIJOIN.                 **/
/***********************************************************************/
    create table one_to_one as
        select m.manunum,
               m.manuname,
               p.prodtype,
               p.prodcost
          from manufacturers  m,
               products        p
         where m.manunum=p.manunum;
/***********************************************************************/
/** ROUTINE..... : ONE-TO-MANY                                           **/
/** PURPOSE..... : Produce a one-to-many data relationship               **/
/**               using the table with the unique key as a               **/
/**               lookup table and a LEFT JOIN.                          **/
/***********************************************************************/
    create table one_to_many as
        select p1.prodnum,
               p1.prodname,
               p2.units,
               p2.unitcost,
               p2.units * p2.unitcost as Total_Cost format=dollar12.2
          from products  p1
               LEFT JOIN
               purchases  p2
             on p1.prodnum=p2.prodnum;
/***********************************************************************/
```

# 282 PROC SQL：使用 SAS 的高级基础，第二版

```sas
/** ROUTINE.....: MANY-TO-ONE **/
/** PURPOSE.....: Produce a many-to-one data relationship **/
/** using a LEFT OUTER JOIN. **/
/*******************************************************************/
create table many_to_one as
select p2.prodnum,
p2.prodname,
p1.units,
p1.unitcost,
p1.units * p1.unitcost as Total_Cost format=dollar12.2
from purchases p1
LEFT JOIN
products p2
on p1.prodnum=p2.prodnum;
```

```sas
/** ROUTINE.....: MANY-TO-MANY **/
/** PURPOSE.....: Produce a many-to-many data relationship **/
/** using the table with the unique key and a **/
/** lookup table in an EQUIJOIN construct. **/
/*******************************************************************/
create table many_to_many as
select p1.prodnum,
p1.prodname,
p2.units,
p2.unitcost,
p2.units * p2.unitcost as Total_Cost format=dollar12.2
from products p1,
purchases p2
where p1.prodnum=p2.prodnum;
quit;
```

结果

一对一、一对多、多对一和多对多数据关系的结果表显示在图 7.5 至图 7.8 中。

## 图 7.5：一对一数据关系

| 制造商编号 | 制造商名称 | 产品类型 | 产品成本 |

| --- | --- | --- | --- |

| 1 | 111 Cupid Computer | Workstation | $3,200.00 |

| 2 | 120 Storage Devices Inc | Workstation | $3,300.00 |

| 3 | 210 Global Comm Corp | Phone | $35.00 |

| 4 | 210 Global Comm Corp | Phone | $175.00 |

| 5 | 500 KPL Enterprises | Software | $299.00 |

| 6 | 500 KPL Enterprises | Software | $399.00 |

| 7 | 500 KPL Enterprises | Software | $299.00 |

| 8 | 500 KPL Enterprises | Software | $299.00 |

## 图 7.6：一对多数据关系

|  | 产品编号 | 产品名称 | 单位 | 单位成本 | 总成本 |

|---|---|---|---|---|---|

| 1 | 1110 Dream Machine | 2 | $3,200.00 | $6,400.00 |

| 2 | 1110 Dream Machine | 1 | $3,200.00 | $3,200.00 |

| 3 | 1110 Dream Machine | 5 | $3,200.00 | $16,000.00 |

| 4 | 1200 Business Machine | 3 | $3,300.00 | $9,900.00 |

| 5 | 1200 Business Machine | 3 | $3,300.00 | $9,900.00 |

| 6 | 1200 Business Machine | 3 | $3,300.00 | $9,900.00 |

| 7 | 1200 Business Machine | 6 | $3,300.00 | $19,800.00 |

| 8 | 1200 Business Machine | 8 | $3,300.00 | $26,400.00 |

| 9 | 1700 Travel Laptop | 2 | $3,400.00 | $6,800.00 |

| 10 | 1700 Travel Laptop | 2 | $3,400.00 | $6,800.00 |

| 11 | 1700 Travel Laptop | 3 | $3,400.00 | $10,200.00 |

| 12 | 1700 Travel Laptop | 7 | $3,400.00 | $23,800.00 |

| 13 | 1700 Travel Laptop | 3 | $3,400.00 | $10,200.00 |

| 14 | 1700 Travel Laptop | 4 | $3,400.00 | $13,600.00 |

| 15 | 1700 Travel Laptop | 5 | $3,400.00 | $17,000.00 |

| 16 | 1700 Travel Laptop | 3 | $3,400.00 | $10,200.00 |

| 17 | 1700 Travel Laptop | 4 | $3,400.00 | $13,600.00 |

| 18 | 1700 Travel Laptop | 2 | $3,400.00 | $6,800.00 |

| 19 | 1700 Travel Laptop | 5 | $3,400.00 | $17,000.00 |

| 20 | 2101 Analog Cell Phone |  |  |  |

| 21 | 2102 Digital Cell Phone | 11 | $175.00 | $1,925.00 |

| ... | ... | ... | ... | ... |

| 47 | 5003 Wordprocessor Software | 9 | $299.00 | $2,691.00 |

| 48 | 5003 Wordprocessor Software | 5 | $299.00 | $1,495.00 |

| 49 | 5003 Wordprocessor Software | 5 | $299.00 | $1,495.00 |

| 50 | 5003 Wordprocessor Software | 7 | $299.00 | $2,093.00 |

| 51 | 5003 Wordprocessor Software | 3 | $299.00 | $897.00 |

| 52 | 5003 Wordprocessor Software | 8 | $299.00 | $2,392.00 |

| 53 | 5003 Wordprocessor Software | 8 | $299.00 | $2,392.00 |

| 54 | 5004 Graphics Software | 3 | $299.00 | $897.00 |

| 55 | 5004 Graphics Software | 1 | $299.00 | $299.00 |

| 56 | 5004 Graphics Software | 3 | $299.00 | $897.00 |

| 57 | 5004 Graphics Software | 2 | $299.00 | $598.00 |

| 58 | 5004 Graphics Software | 2 | $299.00 | $598.00 |

## 图 7.7：多对一数据关系

|  | 产品编号 | 产品名称 | 单位 | 单位成本 | 总成本 |

|---|---|---|---|---|---|

| 1 | 1110 Dream Machine |  | 2 | $3,200.00 | $6,400.00 |

| 2 | 1110 Dream Machine |  | 1 | $3,200.00 | $3,200.00 |

| 3 | 1110 Dream Machine |  | 5 | $3,200.00 | $16,000.00 |

| 4 | 1200 Business Machine |  | 3 | $3,300.00 | $9,900.00 |

| 5 | 1200 Business Machine |  | 3 | $3,300.00 | $9,900.00 |

| 6 | 1200 Business Machine |  | 3 | $3,300.00 | $9,900.00 |

| 7 | 1200 Business Machine |  | 6 | $3,300.00 | $19,800.00 |

| 8 | 1200 Business Machine |  | 8 | $3,300.00 | $26,400.00 |

| 9 | 1700 Travel Laptop |  | 2 | $3,400.00 | $6,800.00 |

| 10 | 1700 Travel Laptop |  | 2 | $3,400.00 | $6,800.00 |

| 11 | 1700 Travel Laptop |  | 3 | $3,400.00 | $10,200.00 |

| 12 | 1700 Travel Laptop |  | 7 | $3,400.00 | $23,800.00 |

| 13 | 1700 Travel Laptop |  | 3 | $3,400.00 | $10,200.00 |

| 14 | 1700 Travel Laptop |  | 4 | $3,400.00 | $13,600.00 |

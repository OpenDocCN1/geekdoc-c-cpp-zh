

## PROC SQL：使用 SAS 的基础知识之外，第二版

```sql
/**
            and the last (max) row within each by-group  **/
/**
            using a subquery.                    **/
/****************************************************************/
    create table between_bygroup_rows as
        select custnum,
                prodnum,
                units,
                unitcost,
                min(prodnum) as Min_Prodnum,
                max(prodnum) as Max_Prodnum,
                'BetweenRow' as ByGroup
        from purchases
            group by custnum
            having CALCULATED min_Prodnum NOT =
                    CALCULATED max_Prodnum AND
                    CALCULATED min_Prodnum NOT =
                        prodnum            AND
                    CALCULATED max_Prodnum NOT = prodnum
            order by custnum, prodnum;
/****************************************************************/
/** ROUTINE.....: CONCATENATE-FIRST-BETWEEN-LAST                **/
/** PURPOSE.....: Concatenate the results from the first (min)  **/
/**
                row, between rows, and last (max) row within  **/
/**
                each by-group using UNION ALL set operators. **/
/****************************************************************/
    create table first_between_last_rows as
        select custnum,
                prodnum,
                units,
                unitcost,
                bygroup
        from first_bygroup_rows
    UNION ALL
        select custnum,
                prodnum,
                units,
                unitcost,
                bygroup
        from between_bygroup_rows
    UNION ALL
        select custnum,
                prodnum,
                units,
                unitcost,
                bygroup
        from last_bygroup_rows;
/****************************************************************/
/** ROUTINE.....: PRINT-FIRST-BETWEEN-LAST                      **/
/** PURPOSE.....: Print the results from the first (min) row,   **/
/**
                between rows, and last (max) row within each  **/
/**
                by-group using a select query.                 **/
```

```sql
/******************************/
reset number;
select *
from first_between_last_rows;
quit;
```

## 结果

FIRST.、LAST. 和 BETWEEN. 行的结果显示在图 7.9 至图 7.11 中。

### 图 7.9：FIRST. 行结果

| Custnum | Prodnum | Units | Unitcost | ByGroup |
|---------|---------|-------|----------|---------|
| 1 | 101 | 1200 | $3,300.00 | FirstRow |
| 2 | 201 | 1700 | $3,400.00 | FirstRow |
| 3 | 301 | 2102 | $175.00 | FirstRow |
| 4 | 401 | 1200 | $3,300.00 | FirstRow |
| 5 | 501 | 1700 | $3,400.00 | FirstRow |
| 6 | 701 | 1110 | $3,200.00 | FirstRow |
| 7 | 801 | 2102 | $175.00 | FirstRow |
| 8 | 901 | 1110 | $3,200.00 | FirstRow |
| 9 | 1001 | 1700 | $3,400.00 | FirstRow |
| 10 | 1101 | 1700 | $3,400.00 | FirstRow |
| 11 | 1201 | 1200 | $3,300.00 | FirstRow |
| 12 | 1301 | 1700 | $3,400.00 | FirstRow |
| 13 | 1401 | 2102 | $175.00 | FirstRow |
| 14 | 1601 | 1700 | $3,400.00 | FirstRow |
| 15 | 1701 | 1110 | $3,200.00 | FirstRow |
| 16 | 1801 | 1700 | $3,400.00 | FirstRow |

### 图 7.10：LAST. 行结果

|  | Custnum | Prodnum | Units | Unitcost | ByGroup |
|---|---|---|---|---|---|
| 1 | 101 | 5004 | 2 | $299.00 | LastRow |
| 2 | 201 | 5003 | 9 | $299.00 | LastRow |
| 3 | 301 | 5001 | 6 | $299.00 | LastRow |
| 4 | 401 | 5004 | 3 | $299.00 | LastRow |
| 5 | 501 | 5004 | 1 | $299.00 | LastRow |
| 6 | 701 | 5004 | 3 | $299.00 | LastRow |
| 7 | 801 | 2102 | 5 | $175.00 | LastRow |
| 8 | 901 | 5004 | 2 | $299.00 | LastRow |
| 9 | 1001 | 1700 | 5 | $3,400.00 | LastRow |
| 10 | 1101 | 2200 | 3 | $130.00 | LastRow |
| 11 | 1201 | 1200 | 8 | $3,300.00 | LastRow |
| 12 | 1301 | 5003 | 5 | $299.00 | LastRow |
| 13 | 1401 | 2102 | 7 | $175.00 | LastRow |
| 14 | 1601 | 1700 | 7 | $3,400.00 | LastRow |
| 15 | 1701 | 1110 | 1 | $3,200.00 | LastRow |
| 16 | 1801 | 1700 | 4 | $3,400.00 | LastRow |

### 图 7.11：BETWEEN. 行结果

|  | Custnum | Prodnum | Units | Unitcost | Min_Prodnum | Max_Prodnum | ByGroup |
|---|---|---|---|---|---|---|---|
| 1 | 101 | 1700 | 5 | $3,400.00 | 1200 | 5004 | BetweenRow |
| 2 | 101 | 2102 | 9 | $175.00 | 1200 | 5004 | BetweenRow |
| 3 | 101 | 5001 | 7 | $299.00 | 1200 | 5004 | BetweenRow |
| 4 | 101 | 5003 | 3 | $299.00 | 1200 | 5004 | BetweenRow |
| 5 | 201 | 2102 | 5 | $175.00 | 1700 | 5003 | BetweenRow |
| 6 | 201 | 5001 | 6 | $299.00 | 1700 | 5003 | BetweenRow |
| 7 | 201 | 5001 | 2 | $299.00 | 1700 | 5003 | BetweenRow |
| 8 | 201 | 5001 | 6 | $299.00 | 1700 | 5003 | BetweenRow |
| 9 | 201 | 5002 | 4 | $399.00 | 1700 | 5003 | BetweenRow |
| 10 | 401 | 1700 | 3 | $3,400.00 | 1200 | 5004 | BetweenRow |
| 11 | 401 | 5001 | 11 | $299.00 | 1200 | 5004 | BetweenRow |
| 12 | 401 | 5002 | 5 | $399.00 | 1200 | 5004 | BetweenRow |
| 13 | 401 | 5003 | 7 | $299.00 | 1200 | 5004 | BetweenRow |
| 14 | 501 | 2102 | 9 | $175.00 | 1700 | 5004 | BetweenRow |
| 15 | 501 | 2102 | 12 | $175.00 | 1700 | 5004 | BetweenRow |
| 16 | 501 | 5001 | 3 | $299.00 | 1700 | 5004 | BetweenRow |
| 17 | 501 | 5003 | 5 | $299.00 | 1700 | 5004 | BetweenRow |
| 18 | 701 | 1200 | 3 | $3,300.00 | 1110 | 5004 | BetweenRow |
| 19 | 701 | 1700 | 2 | $3,400.00 | 1110 | 5004 | BetweenRow |
| 20 | 701 | 5001 | 11 | $299.00 | 1110 | 5004 | BetweenRow |
| 21 | 701 | 5002 | 4 | $399.00 | 1110 | 5004 | BetweenRow |
| 22 | 701 | 5003 | 8 | $299.00 | 1110 | 5004 | BetweenRow |
| 23 | 901 | 1200 | 3 | $3,300.00 | 1110 | 5004 | BetweenRow |
| 24 | 901 | 1700 | 2 | $3,400.00 | 1110 | 5004 | BetweenRow |
| 25 | 901 | 5001 | 9 | $299.00 | 1110 | 5004 | BetweenRow |
| 26 | 901 | 5001 | 2 | $299.00 | 1110 | 5004 | BetweenRow |
| 27 | 901 | 5002 | 5 | $399.00 | 1110 | 5004 | BetweenRow |
| 28 | 901 | 5003 | 8 | $299.00 | 1110 | 5004 | BetweenRow |
| 29 | 1101 | 2102 | 9 | $175.00 | 1700 | 2200 | BetweenRow |
| 30 | 1301 | 2102 | 11 | $175.00 | 1700 | 5003 | BetweenRow |
| 31 | 1301 | 5001 | 3 | $299.00 | 1700 | 5003 | BetweenRow |
| 32 | 1301 | 5002 | 2 | $399.00 | 1700 | 5003 | BetweenRow |

## 确定输入表中的行数

SQL 过程提供用户使用 VERBOSE 选项确定一个或多个输入表贡献的行数的能力。VERBOSE 选项用于在我们寻求了解更多关于输入数据、查询的处理需求以及资源利用率的信息的过程中提供重要的“需要知道”信息，例如输入行数和表的逻辑记录长度。下一个示例显示了一个指定了 SQL 过程 VERBOSE 选项的四表连接查询。

## SQL 代码

```sql
PROC SQL VERBOSE;
    SELECT products.prodname,
        products.prodtype,
        customers.custname,
        manufacturers.manuname
    FROM MANUFACTURERS,
        PRODUCTS,
        INVOICE,
        CUSTOMERS
    WHERE manufacturers.manunum = products.manunum  AND
        manufacturers.manunum = invoice.manunum  AND
        products.prodnum      = invoice.prodnum  AND
        invoice.custnum       = customers.custnum;
QUIT;
```

如以下 SAS 日志所示，当指定 VERBOSE SQL 过程选项时，会为每个表生成有关输入行数以及逻辑记录长度 LRECL 的信息。

## SAS 日志结果

```
PROC SQL VERBOSE;
    SELECT P.prodname,
        P.prodtype,
        C.custname,
        M.manuname
    FROM MANUFACTURERS  M,
        PRODUCTS        P,
        INVOICE         I,
        CUSTOMERS       C
    WHERE M.manunum = P.manunum  AND
        M.manunum = I.manunum  AND
        P.prodnum = I.prodnum  AND
        I.custnum = C.custnum;
Data Set Tags.
Data Set WORK.MANUFACTURERS is num=1 and tag=0001. NOBS=6, lrecl=50.
Data Set WORK.PRODUCTS is num=2 and tag=0002. NOBS=10, lrecl=51.
Data Set WORK.INVOICE is num=3 and tag=0004. NOBS=7, lrecl=20.
Data Set WORK.CUSTOMERS is num=4 and tag=0008. NOBS=18, lrecl=48.
QUIT;
```

## 识别索引最多的表

数据库管理员和用户支持人员关注数据库环境的安装、配置、管理和维护，并因此对包括数据库应用程序的性能和健康状况在内的各种活动特别感兴趣。他们特别需要了解可能影响未来扩展需求的问题。数据库环境中大量索引可能会影响 I/O 和存储性能。因此，我经常发现了解有多少




### 结果

| 发票号码 | 制造商号码 | 客户号码 | 发票数量 - 销售单位 | 发票单价 | 产品号码 |
|---|---|---|---|---|---|
| 1003 | 210 | 101 | 7 | $245.00 | 2101 |

但是，如果所有信息都不在单个表中会怎样？而且如果 Global Comm Corp 的制造商号码未知会怎样？如前所述，连接可以像子查询一样轻松构建。一些用户更喜欢连接而不是子查询，因为连接更容易理解和维护。事实上，连接通常比子查询性能更好。在下一个示例中，Global Comm Corp 的制造商号码未知。因此，需要一个简单的内连接来检索来自 MANUFACTURERS 和 INVOICE 表中与 Global Comm Corp 相关的所有行。

## 简单连接

### SQL 代码

```
PROC SQL;
    SELECT M.manunum, M.manuname, I.invnum,
        I.invqty, I.invprice
    FROM MANUFACTURERS M, INVOICE I
    WHERE M.manunum = I.manunum AND
        M.manuname = 'Global Comm Corp';
QUIT;
```

### 结果

| 制造商号码 | 制造商名称 | 发票号码 | 发票数量 - 销售单位 | 发票单价 |
|---|---|---|---|---|
| 210 | Global Comm Corp | 1003 | 7 | $245.00 |

## 使用子查询传递单个值

让我们看看如何构造一个子查询来提供与连接相同的结果。如前所述，假设你想提取 Global Comm Corp 的所有发票，但只知道制造商名称（或至少是名称的一部分），而不知道制造商号码（MANUNUM）。以下子查询在其外部查询 WHERE 子句中使用 =（等于号）来实现这一点。

由于制造商号码未知，因此构造了一个子查询来首先在 MANUFACTURERS 表中搜索制造商号码。实际上，子查询方法比之前的查询方法更灵活，因为它不需要唯一的制造商号码，而制造商号码通常比制造商名称更难记住。它还能够在制造商号码发生变化时进行快速搜索。

当整个查询执行时，SQL 首先评估外部查询 WHERE 子句中的内部查询（或子查询）。它以与独立查询相同的方式执行内部查询。它在 MANUFACTURERS 表中搜索制造商名称等于字符字符串 Global Comm Corp 的任何行，然后提取该行的 MANUNUM 值。SQL 然后将从内部查询派生的 MANUNUM 值 210 代入主查询（外部查询）谓词中。由此产生的替换使 SQL 查询看起来与前面提到的查询完全相同。

### SQL 代码

```
PROC SQL;
    SELECT *
    FROM INVOICE
    WHERE manunum =
        (SELECT manunum
         FROM MANUFACTURERS
         WHERE manuname = 'Global Comm Corp');
QUIT;
```

### 生成的查询

```
PROC SQL;
    SELECT *
    FROM INVOICE
    WHERE manunum = 210;
QUIT;
```

1. PROC SQL 评估外部查询 WHERE 子句中的内部查询，以搜索制造商 Global Comm Corp 的制造商号码。
2. 在将从内部查询派生的制造商号码值代入后生成的查询评估为单个值，然后作为主（外部）查询执行。

### 结果

| 发票号码 | 制造商号码 | 客户号码 | 发票数量 - 销售单位 | 发票单价 | 产品号码 |
|---|---|---|---|---|---|
| 1003 | 210 | 101 | 7 | $245.00 | 2101 |

让我们再看一个子查询。假设你想从 INVOICE 表中检索制造 Dream Machine 工作站的制造商的发票。以下子查询（内部查询）提取与 Dream Machine 关联的产品号码（PRODNUM），并将单个值传递给外部查询进行处理。

### SQL 代码

```
PROC SQL FEEDBACK;
    SELECT *
    FROM INVOICE
    WHERE prodnum =
        (SELECT prodnum
         FROM PRODUCTS
         WHERE prodname LIKE 'Dream%');
QUIT;
```

### 生成的查询

```
PROC SQL;
    SELECT *
    FROM INVOICE
    WHERE prodnum = 1110;
QUIT;
```

1. PROC SQL 评估外部查询 WHERE 子句中的内部查询，以搜索 Dream Machine 产品对应的产品号码。
2. 在将派生的产品号码值代入后生成的查询然后作为主（外部）查询执行。

### 结果

| 发票号码 | 制造商号码 | 客户号码 | 发票数量 - 销售单位 | 发票单价 | 产品号码 |
|---|---|---|---|---|---|
| 1004 | 111 | 501 | 3 | $9,600.00 | 1110 |

很幸运的是，前一个示例中的子查询只向主（外部）查询传递了一行或一个值。如果它从 PRODUCTS 表返回多于一个值，则 SQL 过程将无法将条件评估为真或假，并会在外部查询中产生错误。让我们再看一个子查询返回多于一个值的示例。

在下一个示例中，内部查询返回多于一行，使主查询无法评估为真或假。因此，产生错误，外部查询未执行。一般来说，最好避免在子查询表达式中使用 =（等于号）和其他比较运算符（<、>、<=、>= 和 <>），除非你事先知道子查询的结果是一个包含单行数据的表（尽管有时可能无法提前知道这一点）。在本章“使用子查询传递多于一行”部分中，你将看到通过使用 IN 谓词解决了此问题。

### SQL 代码

```
PROC SQL;
    SELECT *
    FROM INVOICE
    WHERE manunum =
        (SELECT manunum
         FROM MANUFACTURERS
         WHERE UPCASE(manucity) LIKE 'SAN DIEGO%');
QUIT;
```

### SAS 日志结果

```
PROC SQL;
    SELECT *
    FROM INVOICE
    WHERE manunum =
        (SELECT manunum
         FROM MANUFACTURERS
         WHERE UPCASE(manucity) LIKE 'SAN DIEGO%');
ERROR: Subquery evaluated to more than one row.
QUIT;
NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE SQL used:
      real time 0.00 seconds
```

让我们再看一个使用比较运算符 <（小于）的子查询示例。内部查询中指定的汇总函数强制产生单行结果。在下一个示例中，子查询使用 AVG 汇总（聚合）函数来确定哪些产品（基于其发票数量）购买量低于平均产品购买量。

### SQL 代码

```
PROC SQL;
    SELECT prodnum, invnum, invqty, invprice
    FROM INVOICE
    WHERE invqty <
        (SELECT AVG(invqty)
         FROM INVOICE);
QUIT;
```

### 生成的查询

```
PROC SQL;
    SELECT prodnum, invnum, invqty, invprice
    FROM INVOICE
    WHERE invqty < 4.285714;
QUIT;
```

1. PROC SQL 评估外部查询 WHERE 子句中的内部查询以生成平均发票数量。
2. 生成的查询将派生的平均发票数量 4.285714 作为单个值传递给主（外部）查询以供执行。

### 结果

| 产品号码 | 发票号码 | 发票数量 - 销售单位 | 发票单价 |
|---|---|---|---|
| 6001 | 1002 | 2 | $1,598.00 |
| 1110 | 1004 | 3 | $9,600.00 |
| 5002 | 1005 | 2 | $798.00 |
| 6000 | 1006 | 4 | $396.00 |

## 使用子查询传递多于一行

PROC SQL 不允许子查询选择多于一列。为了防止与向主（外部）查询传递多于一个值相关的问题，可以在子查询中指定 IN 谓词。与 DATA 步中的 IN 运算符类似，IN 谓词允许 SQL 过程将多个行值从（内部）子查询传递到主（外部）查询而不产生错误。

下一个示例展示了如何使用 IN 谓词将多个行值从子查询传递到主（外部）查询，用于 San Diego 制造商。

### SQL 代码

```
PROC SQL;
    SELECT *
    FROM INVOICE
    WHERE manunum IN
        (SELECT manunum
         FROM MANUFACTURERS
         WHERE UPCASE(manucity) LIKE 'SAN DIEGO%');
QUIT;
```

### 生成的查询

```
PROC SQL;
    SELECT *
    FROM INVOICE
    WHERE manunum IN (210, 500, 700);
QUIT;
```

1. PROC SQL 的 IN 谓词在外部查询中指定，以处理从内部查询传递的值列表。


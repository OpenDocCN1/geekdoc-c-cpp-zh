
```
PROC SQL;
    SELECT products.prodname,
        products.prodtype,
        customers.custname,
        manufacturers.manuname
    FROM MANUFACTURERS,
        PRODUCTS,
        INVOICE,
        CUSTOMERS
    WHERE manufacturers.manunum = products.manunum AND
        manufacturers.manunum = invoice.manunum AND
        products.prodnum = invoice.prodnum AND
        invoice.custnum = customers.custnum;
QUIT;
```

### 结果

| 产品名称 | 产品类型 | 客户名称 | 制造商名称 |

|---|---|---|---|

| 模拟手机 | 电话 | La Mesa Computer Land | Global Comm Corp |

| 电子表格软件 | 软件 | Vista Tech Center | KPL Enterprises |

| 梦幻机器 | 工作站 | Alpine Technical Center | Cupid Computer |

| 数据库软件 | 软件 | Jamul Hardware & Software | KPL Enterprises |

## 外连接

如本章前面的示例所示，内连接会忽略不满足搜索条件的任何行。这与外连接分组表的方式有很大不同。与内连接相反，外连接保留符合`ON`（搜索）条件的行，同时保留来自一个或两个表中部分或全部不匹配的数据。本质上，外连接保留一个表中的行，即使它们与第二个表中的行不匹配。这一区别至关重要，因为它真正区分了外连接和内连接。

其次，外连接一次最多能处理两个表，而（在SAS实现下）内连接最多能处理256个表。

另一个区别与外连接的语法指定方式有关。在内连接的`FROM`子句中用于将一个表与另一个表分隔开的逗号，在外连接中被以下关键字之一替换：`LEFT JOIN`、`RIGHT JOIN`或`FULL JOIN`。此外，用于限制结果表中保留行的`WHERE`子句表达式被替换为`ON`关键字。

最后，外连接被认为是一种不对称连接（Lorie, Raymond A., 和 Jean-Jacques Daudenarde, SQL & Its Applications, 第87页）。与内连接不同，外连接不会从其组成部分或表中按比例选择行。

## 左外连接

让我们看看左连接在现实世界中的应用场景。假设你想查看所有制造商、其所在城市、制造商编号、产品类型和产品成本（如果有），而不遗漏那些还没有产品的制造商。这意味着`MANUFACTURERS`表（左表）作为主表，保留其行，而`PRODUCTS`表（右表）作为从表（附属表）。下面的左外连接示例有效地保留了来自两个表的匹配行，以及保留了左表中在右表中没有匹配的行。

### SQL 代码

```
PROC SQL;
    SELECT manuname, manucity, manufacturers.manunum,
        products.prodtype, products.prodcost
    FROM MANUFACTURERS LEFT JOIN PRODUCTS
        ON manufacturers.manunum =
            products.manunum;
QUIT;
```

① `LEFT JOIN`规范保留左表（`MANUFACTURERS`）中的所有行，即使右表（`PRODUCTS`）中没有匹配的行。

② `ON`子句充当`WHERE`子句，在连接结果中选择所需行。

如左外连接结果所示，左（`MANUFACTURERS`）表中与右（`PRODUCTS`）表中行匹配的行被包含在结果表中。因此，有8行匹配，这可以通过分配给产品类型和产品成本的值来证明。此外，左表中与右表中行不匹配（基于搜索条件）的两行也被保留（加粗显示）。因此，`MANUFACTURERS`表中在`PRODUCTS`表中没有匹配值的每一行都会被添加到结果虚拟表中，并在产品类型和产品成本列中带有空值。

### 结果

| 制造商名称 | 制造商城市 | 制造商编号 | 产品类型 | 产品成本 |

| Cupid Computer | 休斯顿 | 111 | 工作站 | $3,200.00 |

| Storage Devices Inc | 圣马特奥 | 120 | 工作站 | $3,300.00 |

| Global Comm Corp | 圣地亚哥 | 210 | 电话 | $175.00 |

| Global Comm Corp | 圣地亚哥 | 210 | 电话 | $35.00 |

| KPL Enterprises | 圣地亚哥 | 500 | 软件 | $299.00 |

| KPL Enterprises | 圣地亚哥 | 500 | 软件 | $299.00 |

| KPL Enterprises | 圣地亚哥 | 500 | 软件 | $299.00 |

| KPL Enterprises | 圣地亚哥 | 500 | 软件 | $399.00 |

| World Internet Corp | 迈阿密 | 600 |  | . |

| San Diego PC Planet | 圣地亚哥 | 700 |  | . |

## 指定 `WHERE` 子句

为了提供更大的子集功能以及增加灵活性，SQL 过程在构造外连接时除了 `ON` 子句外，还允许指定可选的 `WHERE` 子句。能够在外连接中结合 `ON` 子句指定 `WHERE` 子句，可以更好地控制行的子集。一个示例将有助于说明 `WHERE` 子句在外连接中的用法。假设您想将之前的左外连接的结果限制为仅成本低于 $300.00 的产品。在此示例中，左外连接语法使用 `WHERE` 子句将行结果子集化为非缺失且成本低于 $300.00 的产品。

### SQL 代码

```
PROC SQL;
    SELECT manuname, manucity, manufacturers.manunum,
            products.prodtype, products.prodcost
    FROM MANUFACTURERS LEFT JOIN PRODUCTS
    ON manufacturers.manunum =
        products.manunum
    WHERE prodcost < 300 AND
        prodcost NE .;
QUIT;
```

在外连接中除了 `ON` 子句之外指定的可选 `WHERE` 子句，进一步对连接结果进行子集化。

### 结果

| Manufacturer Name | Manufacturer City | Manufacturer Number | Product Type | Product Cost |

|---|---|---|---|---|

| Global Comm Corp | San Diego | 210 | Phone | $175.00 |

| Global Comm Corp | San Diego | 210 | Phone | $35.00 |

| KPL Enterprises | San Diego | 500 | Software | $299.00 |

| KPL Enterprises | San Diego | 500 | Software | $299.00 |

| KPL Enterprises | San Diego | 500 | Software | $299.00 |

## 指定聚合函数

假设您需要生成一份按制造商汇总的月度发票金额报告。可以使用外连接语法指定聚合函数，结合 `GROUP BY` 子句执行分组计算。在下一个示例中，左连接使用 `SUM` 函数和 `GROUP BY` 子句计算每个制造商的总发票金额。

### SQL 代码

```
PROC SQL;
    SELECT manuname,
        SUM(invoice.invprice) AS Total_Invoice_Amt
            FORMAT=DOLLAR10.2
        FROM MANUFACTURERS LEFT JOIN INVOICE
        ON manufacturers.manunum =
            invoice.manunum
        GROUP BY MANUNAME;
QUIT;
```

- `SUM`函数计算每个制造商的总发票金额。

- `GROUP BY`子句将与制造商关联的所有行分组为单行。

结果显示，没有活动的制造商在聚合的 `Total_Invoice_Amt` 列中具有空值或缺失值。

### 结果

| Manufacturer Name | Total_Invoice_Amt |

|---|---|

| Cupid Computer | $9,600.00 |

| Global Comm Corp | $245.00 |

| KPL Enterprises | $25,789.00 |

| San Diego PC Planet | . |

| Storage Devices Inc | . |

| World Internet Corp | $1,598.00 |

## 右外连接

右连接与左连接类似，只是保留右侧（第二个）表中的行。因此，结果包含对称连接的行加上右侧表中每个未匹配行的行。左表的值会自动用空值替代。假设您想查看所有制造商及其各自的产品。在下一个示例中，使用右外连接构造从 `PRODUCTS` 和 `MANUFACTURERS` 表生成包含产品、产品类型、制造商编号和制造商名称的简单报告。

### SQL 代码

```
PROC SQL;
    SELECT prodname, prodtype,
        products.manunum, manuname
    FROM PRODUCTS RIGHT JOIN MANUFACTURERS
        ON products.manunum = manufacturers.manunum;
QUIT;
```

- `RIGHT JOIN`规范保留右侧表（`MANUFACTURERS`）中的所有行，即使左侧表（`PRODUCTS`）中没有匹配行。

结果显示，在 `MANUFACTURERS` 表中出现但在 `PRODUCTS` 表中没有列出产品的制造商，其产品名称、产品类型和制造商编号列中具有空值或缺失值。

Note: 要从结果中删除具有缺失值的行，可以指定 `WHERE` 子句。

### 结果

| Product Name | Product Type | Manufacturer Number | Manufacturer Name |

| Dream Machine | Workstation | 111 | Cupid Computer |

| Business Machine | Workstation | 120 | Storage Devices Inc |

| Digital Cell Phone | Phone | 210 | Global Comm Corp |

| Analog Cell Phone | Phone | 210 | Global Comm Corp |

| Spreadsheet Software | Software | 500 | KPL Enterprises |

| Graphics Software | Software | 500 | KPL Enterprises |

| Wordprocessor Software | Software | 500 | KPL Enterprises |

| Database Software | Software | 500 | KPL Enterprises |

|  |  | . | World Internet Corp |

|  |  | . | San Diego PC Planet |

## 全外连接

全外连接通过保留左侧和右侧表中的行，结合了左连接和右连接的强大功能。虽然全连接不像左连接或右连接构造那样常用，但在两个表的信息都缺失时可能很有用。在下一个示例中，指定全外连接以生成包含没有产品的制造商和没有已知制造商的产品的报告。

### SQL 代码

```
PROC SQL;
    SELECT prodname, prodtype,
        products.manunum, manuname
    FROM PRODUCTS FULL JOIN MANUFACTURERS
        ON products.manunum =
            manufacturers.manunum;
QUIT;
```

- 全连接规范保留左侧表（`PRODUCTS`）中的所有行以及右侧表（`MANUFACTURERS`）中的所有行，即使没有匹配行。

### 结果

| Product Name | Product Type | Manufacturer Number | Manufacturer Name |

|---|---|---|---|

| Dream Machine | Workstation | 111 | Cupid Computer |

| Business Machine | Workstation | 120 | Storage Devices Inc |

| Travel Laptop | Laptop | 170 |  |

| Digital Cell Phone | Phone | 210 | Global Comm Corp |

| Analog Cell Phone | Phone | 210 | Global Comm Corp |

| Office Phone | Phone | 220 |  |

| Spreadsheet Software | Software | 500 | KPL Enterprises |

| Graphics Software | Software | 500 | KPL Enterprises |

| Wordprocessor Software | Software | 500 | KPL Enterprises |

| Database Software | Software | 500 | KPL Enterprises |

|  |  | . | World Internet Corp |

|  |  | . | San Diego PC Planet |

## 子查询

现在您已经了解了如何通过连接查询组合两个或多个表，请将注意力转向另一种复杂查询类型，即子查询。子查询是嵌套在另一个查询表达式中的查询表达式。其目的是让内部查询产生一个值或多个值，然后将其传递给外部查询进行处理。您可以通过将`SELECT`语句嵌入外部查询的`SELECT`语句、`INSERT`语句、`DELETE`语句或`HAVING`子句的`WHERE`子句中来实现此目的。

Note: 由于这会引入概念和处理上的复杂性，您应避免嵌套超过两层子查询。

典型的子查询由（内部）查询与另一个（外部或主）查询的谓词中组合而成。处理时，内部查询将布尔值传递给外部查询，如果返回至少一行则为 True，如果子查询未返回任何行则为 False。内部查询的结果存储在临时结果表中，并用作主查询的输入。我们对子查询的探索将涉及使用比较运算符、`IN`谓词以及`ANY`和`ALL`关键字，并将以一种称为相关子查询的特殊子查询类型结束。

## 子查询的替代方法

子查询是一个非常有用的构造，尤其是在需要关联来自多个表的信息时。不幸的是，子查询并不总是容易构造，而且可能更难理解。因此，在用子查询构造每个表关系之前，请仔细考虑您的选择。

当所有信息都可用在单个表中时，简单的查询可能就是所需全部。假设您想生成一份由 Global Comm Corp 组成的发票信息报告。让我们进一步假设您知道 Global Comm Corp 的特定制造商编号。知道这一点意味着您不必进入 `MANUFACTURERS` 表去查找它。在下一个示例中，构造一个简单查询以从 `INVOICE` 表检索所有发票信息。

### 简单查询

```
PROC SQL;
    SELECT *
        FROM INVOICE
        WHERE manunum = 210;
QUIT;
```

#### 结果

| 发票号码 | 制造商号码 | 客户号码 | 发票数量 - 销售单位 | 发票单价 | 产品号码 |

|---|---|---|---|---|---|

| 1003 | 210 | 101 | 7 | $245.00 | 2101 |

但是，如果所有信息都不在单个表中会怎样？而且如果 Global Comm Corp 的制造商号码未知会怎样？如前所述，连接可以像子查询一样轻松构建。一些用户更喜欢连接而不是子查询，因为连接更容易理解和维护。事实上，连接通常比子查询性能更好。在下一个示例中，Global Comm Corp 的制造商号码未知。因此，需要一个简单的内连接来检索来自 `MANUFACTURERS` 和 `INVOICE` 表中与 Global Comm Corp 相关的所有行。

### 简单连接

#### SQL 代码

```
PROC SQL;
    SELECT M.manunum, M.manuname, I.invnum,
        I.invqty, I.invprice
    FROM MANUFACTURERS M, INVOICE I
    WHERE M.manunum = I.manunum AND
        M.manuname = 'Global Comm Corp';
QUIT;
```

#### 结果

| 制造商号码 | 制造商名称 | 发票号码 | 发票数量 - 销售单位 | 发票单价 |

|---|---|---|---|---|

| 210 | Global Comm Corp | 1003 | 7 | $245.00 |

## 使用子查询传递单个值


① `DISTINCT` 关键字可防止重复行出现在结果中。

### 结果

| Total_Cost | Manufacturer Number |
|---|---|
| $1,296.00 | 500 |

## 非等值连接

另一种内连接类型称为非等值连接。正如其名称所示，非等值连接在其 `WHERE` 子句中没有指定等号`=`。例如，

假设您想要显示由 KPL 企业制造的、成本超过 299.00 美元的产品。使用大于号`>`运算符，这种类型的连接由此得名。

注意：当 SQL 过程优化器无法通过减少笛卡尔积来优化连接查询时，SAS 日志中会显示一条消息，表明该连接需要执行一个或多个笛卡尔积连接，且无法优化。

### SQL 代码

```
PROC SQL;
    SELECT prodname, prodtype, prodcost,
            manufacturers.manunum, manufacturers.manuname
    FROM PRODUCTS, MANUFACTURERS
    WHERE manufacturers.manunum = 500 AND
          prodtype = 'Software' AND
          prodcost > 299.00;
QUIT;
```

① 在 `WHERE` 子句中指定大于号`>`运算符表示非等值连接场景。

## SAS 日志结果

```
PROC SQL;
    SELECT prodname, prodtype, prodcost,
            manufacturers.manunum, manufacturers.manuname
    FROM PRODUCTS, MANUFACTURERS
    WHERE manufacturers.manunum = 500 AND
          prodtype = 'Software' AND
          prodcost > 299.00;
NOTE: The execution of this query involves performing one or more Cartesian product joins that cannot be optimized.
    QUIT;
NOTE: PROCEDURE SQL used:
      real time           0.01 seconds
      cpu time            0.01 seconds
```

### 结果

| 产品名称 | 产品类型 | 产品成本 | 制造商编号 | 制造商名称 |
|---|---|---|---|---|
| 数据库软件 | 软件 | $399.00 | 500 | KPL 企业 |

## 反射连接或自连接

最后一种内连接类型称为反射连接（reflexive join），也称为自连接（self join）。顾名思义，自连接会创建表的一个内部副本，然后将该副本与自身连接。本质上，这种连接是将表的一个副本与自身连接，以便利用和展示表值之间的比较。例如，假设您希望按产品类型并排比较产品价格，价格较低的产品排在前面（如示例结果的前三列所示）。

### SQL 代码

```
PROC SQL;
    SELECT products.prodname, products.prodtype,
            products.prodcost,
            products_copy.prodname, products_copy.prodtype,
            products_copy.prodcost
        FROM PRODUCTS, PRODUCTS PRODUCTS_COPY
        WHERE products.prodtype =
                products_copy.prodtype AND
                products.prodcost <
                products_copy.prodcost;
QUIT;
```

1 `PRODUCTS` 表是在 `FROM` 子句中指定的主表。

2 名为 `PRODUCTS_COPY` 的 `PRODUCTS` 表副本与 `PRODUCTS` 表连接。

3 `WHERE` 子句要求对相同类型的产品进行并排比较，价格较低的产品排在最前面。

### 结果

| 产品名称 | 产品类型 | 产品成本 | 产品名称 | 产品类型 | 产品成本 |
|---|---|---|---|---|---|
| 梦幻机 | 工作站 | $3,200.00 | 商务机 | 工作站 | $3,300.00 |
| 模拟手机 | 电话 | $35.00 | 办公电话 | 电话 | $130.00 |
| 模拟手机 | 电话 | $35.00 | 数字手机 | 电话 | $175.00 |
| 办公电话 | 电话 | $130.00 | 数字手机 | 电话 | $175.00 |
| 电子表格软件 | 软件 | $299.00 | 数据库软件 | 软件 | $399.00 |
| 文字处理软件 | 软件 | $299.00 | 数据库软件 | 软件 | $399.00 |
| 图形软件 | 软件 | $299.00 | 数据库软件 | 软件 | $399.00 |

让我们看另一个示例。假设您想查找客户名称和发票金额，并针对每位客户列出发票金额更大的客户名称和发票金额。下一个示例展示了自连接的一个有用应用。

### SQL 代码

```
PROC SQL;
SELECT invoice.custnum, invoice.invprice,
    invoice_copy.custnum, invoice_copy.invprice
FROM INVOICE, INVOICE INVOICE_COPY
WHERE invoice.invprice <
    invoice_copy.invprice;
QUIT;
```

- ① `INVOICE` 表是在 `FROM` 子句中指定的主表。

- ② 名为 `INVOICE_COPY` 的 `INVOICE` 表副本与 `INVOICE` 表连接。

- ③ `WHERE` 子句生成发票金额更大的客户名称。

### 结果

| 客户编号 | 发票单价 | 客户编号 | 发票单价 |
|---|---|---|---|
| 201 | $1,495.00 | 1301 | $1,598.00 |
| 201 | $1,495.00 | 501 | $9,600.00 |
| 201 | $1,495.00 | 401 | $23,100.00 |
| 1301 | $1,598.00 | 501 | $9,600.00 |
| 1301 | $1,598.00 | 401 | $23,100.00 |
| 101 | $245.00 | 201 | $1,495.00 |
| 101 | $245.00 | 1301 | $1,598.00 |
| 101 | $245.00 | 501 | $9,600.00 |
| 101 | $245.00 | 801 | $798.00 |
| 101 | $245.00 | 901 | $396.00 |
| 101 | $245.00 | 401 | $23,100.00 |
| 501 | $9,600.00 | 401 | $23,100.00 |
| 801 | $798.00 | 201 | $1,495.00 |
| 801 | $798.00 | 1301 | $1,598.00 |
| 801 | $798.00 | 501 | $9,600.00 |
| 801 | $798.00 | 401 | $23,100.00 |
| 901 | $396.00 | 201 | $1,495.00 |
| 901 | $396.00 | 1301 | $1,598.00 |
| 901 | $396.00 | 501 | $9,600.00 |
| 901 | $396.00 | 801 | $798.00 |
| 901 | $396.00 | 401 | $23,100.00 |

## 在连接中使用表别名

SAS 库中的每个表都必须有唯一的名称以供引用。表名称必须符合有效的 SAS 命名约定，这意味着表名称的最大长度可以为 32 个字符，并且必须以字母或下划线开头（有关更多详细信息，请参阅《SAS 语言参考：概念》）。

为了减少引用连接查询中指定表所需的击键次数，可以为每个表指定一个别名或临时表名称引用。指定后，这些任意别名提供了对表本身的快捷方式，并且在连接查询期间有效，但之后不再有效。在下一个示例中，在 `FROM` 子句中，将表别名`P`分配给 `PRODUCTS` 表，将别名`M`分配给 `MANUFACTURERS` 表。`SELECT` 语句和 `WHERE` 子句中的表名称引用也变得更加容易。

### SQL 代码

```
PROC SQL;
    SELECT prodnum, prodname, prodtype, M.manunum
        FROM PRODUCTS  P, MANUFACTURERS  M
            WHERE P.manunum  = M.manunum AND
                M.manuname  = 'KPL Enterprises';
QUIT;
```

① 在 `FROM` 子句中分配表别名`P`和表别名`M`，为引用较长的表名 `PRODUCTS` 和 `MANUFACTURERS` 提供了快捷方式。

### 结果

| 产品编号 | 产品名称 | 产品类型 | 制造商编号 |
|---|---|---|---|
| 5001 | 电子表格软件 | 软件 | 500 |
| 5002 | 数据库软件 | 软件 | 500 |
| 5003 | 文字处理软件 | 软件 | 500 |
| 5004 | 图形软件 | 软件 | 500 |

## 在连接中执行计算

连接查询与较简单的查询一样，可以充分利用 SQL 过程的功能。逻辑和算术运算符、谓词和汇总函数都可以供您使用。连接查询是必不可少的组件，因为存储的信息并非总是以您需要的形式提供。

`PROC SQL` 提供了对包含数值的列执行基本算术运算的能力，例如加、减、乘、除。本质上，这使任何查询都能执行列加法、减法、乘法和除法。假设您想计算在加利福尼亚州销售的所有制造产品的 7.75% 的销售税。在下一个示例中，`SELECT` 语句显示加利福尼亚销售税的计算（使用产品成本列和固定销售税百分比），并为结果列分配列别名以及格式和标签，以增强结果的可读性。

### SQL 代码

```
PROC SQL;
    SELECT prodname, prodtype, prodcost,
        prodcost * .0775 AS SalesTax
        FORMAT=dollar10.2 LABEL='California Sales Tax'
    FROM PRODUCTS P, MANUFACTURERS M
        WHERE P.manunum = M.manunum AND
            M.manustat = 'CA';
QUIT;
```

① 在 `SELECT` 语句中执行基本算术运算以及为结果分配列别名的能力是 SQL ANSI 标准的一部分。

### 结果

| 产品名称 | 产品类型 | 产品成本 | 加利福尼亚销售税 |
|---|---|---|---|
| 商务机 | 工作站 | $3,300.00 | $255.75 |
| 模拟手机 | 电话 | $35.00 | $2.71 |
| 数字手机 | 电话 | $175.00 | $13.56 |
| 电子表格软件 | 软件 | $299.00 | $23.17 |
| 数据库软件 | 软件 | $399.00 | $30.92 |
| 文字处理软件 | 软件 | $299.00 | $23.17 |
| 图形软件 | 软件 | $299.00 | $23.17 |

## 三表连接

到目前为止，我们的示例仅限于两表连接。但如果需要的信息超出两个表所能提供的范围怎么办？要提取所需的信息，可能需要访问第三个表。三表连接是两表连接的相当简单的扩展。

与之前一样，每个可连接的列必须具有相同的列属性，并包含相同类型的信息。除了在 `FROM` 子句中列出所有必需的表之外，`WHERE` 子句还需要包含所有限制条件，以便仅对所需行进行子集化。例如，假设您只想显示在 `INVOICE` 表中出现、制造商为 KPL 企业（`manunum=500`）的那些产品及其发票数量。

252 PROC SQL：使用SAS超越基础（第二版）

```
PROC SQL;
SELECT P.prodname,
P.prodcost,
M.manuname,
I.invqty
FROM PRODUCTS P,
MANUFACTURERS M,
INVOICE I
WHERE P.manunum = M.manunum AND
P.prodnum = I.prodnum AND
M.manunum = 500;
QUIT;
```

| 产品名称 | 产品成本 | 制造商名称 | 发票数量—已售单位 |
|---|---|---|---|
| 电子表格软件 | $299.00 | KPL Enterprises | 5 |
| 数据库软件 | $399.00 | KPL Enterprises | 2 |

让我们进一步研究一下这个三表连接的 `WHERE` 子句的构造。`PRODUCTS`、`MANUFACTURERS` 和 `INVOICE` 表中包含制造商编号的列，通过 `WHERE` 子句中的 `AND` 逻辑运算符进行连接。此外，`WHERE` 子句将结果表限制为仅包含制造商（`manunum=500`）的产品发票。在下一个示例中，三表连接列出了产品名称和成本，以及购买每种产品的客户。

```
PROC SQL;
SELECT P.prodname,
P.prodcost,
C.custprice,
I.invprice
FROM PRODUCTS P,
INVOICE I,
CUSTOMERS C
WHERE P.prodnum = I.prodnum AND
I.custnum = C.custnum;
QUIT;
```

### 结果

| 产品名称 | 产品成本 | 客户名称 | 发票单价 |
|---|---|---|---|
| 模拟手机 | $35.00 | La Mesa Computer Land | $245.00 |
| 电子表格软件 | $299.00 | Vista Tech Center | $1,495.00 |
| 商用机器 | $3,300.00 | La Jolla Computing | $23,100.00 |
| 梦幻机器 | $3,200.00 | Alpine Technical Center | $9,600.00 |
| 数据库软件 | $399.00 | Jamul Hardware & Software | $798.00 |

## 超过三个表的连接

有时，需要从四个、五个或更多表（最多256个表）中提取信息。四个或更多表的连接可以像访问两个或三个表一样构造。唯一的区别是 `FROM` 子句中表引用的数量以及 `WHERE` 子句中限制保留行的复杂性。假设你想根据发票知道在2000年9月1日之前订购的产品数量。一种查找此信息的方法是执行四表连接。

## SQL 代码

```
PROC SQL;
    SELECT sum(inventory.invenqty)
        AS Products_Ordered_Before_09012000
    FROM PRODUCTS,
        INVOICE,
        CUSTOMERS,
        INVENTORY
    WHERE inventory.orddate < mdy(09,01,00) AND
        products.prodnum = invoice.prodnum AND
        invoice.custnum = customers.custnum AND
        invoice.prodnum = inventory.prodnum;
QUIT;
```

### 结果

| 2000年9月1日前订购的产品数量 |
|---|
| 8 |

如果你想知道这个结果是否可以用另一种方式得出，那你猜对了。你也可以使用以下两表连接代码，根据发票确定在2000年9月1日之前订购的产品数量。与这个示例一样，通常有不止一种构造连接来提取所需信息的方法。

## SQL 代码

```
PROC SQL;
    SELECT sum(inventory.invenqty)
        AS Products_Ordered_Before_09012000
    FROM INVOICE I,
        INVENTORY I2
    WHERE inventory.orddate < mdy(09,01,00) AND
        invoice.prodnum = inventory.prodnum;
QUIT;
```

### 结果

![](img/9d3e4d8fa063e50a0c9985e34cf9d6e8_276_0.png)

为了加深你对超过三个表连接的理解，下面的示例说明了一个四表连接。假设你想知道哪些产品正在被购买以及谁在购买它们。下一个示例展示了连接 `MANUFACTURERS`、`PRODUCTS`、`INVOICE` 和 `CUSTOMERS` 表的四向内连接。

## SQL 代码

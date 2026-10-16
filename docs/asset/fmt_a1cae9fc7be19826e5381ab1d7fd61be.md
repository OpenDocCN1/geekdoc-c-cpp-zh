
```
PROC SQL;
    SELECT CATX(',', ', ', manucity, manustat)
        As Headquarters
    FROM MANUFACTURERS;
QUIT;
```

## Results

![](img/9d3e4d8fa063e50a0c9985e34cf9d6e8_123_0.png)

## Using Scalar Expressions with Selected Columns

在计算术语中，标量是指由单个数字或值表示的数量。该值不是表示为数组或值列表，而是作为单个值。例如，值 7 是标量值，但 (0,0,7) 不是。`PROC SQL` 允许使用标量表达式和常量与所选列一起使用。通常，这些表达式替换或增强 `SELECT` 语句中的一个或多个列。为了说明标量表达式的使用，假设 `PRODUCTS` 表中每个产品的销售税百分比为 7.5%。结果包括产品名称、产品成本和派生的计算销售税列。

注意：尽管计算列包含每个产品的销售税计算结果，但它不包含列标题。

### SQL Code

```
PROC SQL;
    SELECT prodname, prodcost,
        .075 * prodcost
    FROM PRODUCTS;
QUIT;
```

### Results

| Product Name | Product Cost |  |
|---|---|---|
| Dream Machine | $3,200.00 | 240 |
| Business Machine | $3,300.00 | 247.5 |
| Travel Laptop | $3,400.00 | 255 |
| Analog Cell Phone | $35.00 | 2.625 |
| Digital Cell Phone | $175.00 | 13.125 |
| Office Phone | $130.00 | 9.75 |
| Spreadsheet Software | $299.00 | 22.425 |
| Database Software | $399.00 | 29.925 |
| Wordprocessor Software | $299.00 | 22.425 |
| Graphics Software | $299.00 | 22.425 |

在接下来的两个示例中，为在前一个示例中计算的派生销售税列分配列标题或别名。实现此目的存在两种方法。如下一个示例所示，第一种方法使用 `AS` 关键字为派生列分配名称，并允许在查询中稍后引用该列。

### SQL Code

```
PROC SQL;
    SELECT prodname, prodcost,
        .075 * prodcost AS Sales_Tax
    FROM PRODUCTS;
QUIT;
```

### Results

**The SAS System**

| Product Name | Product Cost | Sales_Tax |
|---|---|---|
| Dream Machine | $3,200.00 | 240 |
| Business Machine | $3,300.00 | 247.5 |
| Travel Laptop | $3,400.00 | 255 |
| Analog Cell Phone | $35.00 | 2.625 |
| Digital Cell Phone | $175.00 | 13.125 |
| Office Phone | $130.00 | 9.75 |
| Spreadsheet Software | $299.00 | 22.425 |
| Database Software | $399.00 | 29.925 |
| Wordprocessor Software | $299.00 | 22.425 |
| Graphics Software | $299.00 | 22.425 |

下一个示例说明了为计算的销售税列分配列标题的第二种方法，使用 `LABEL=` 选项。为了进一步增强输出的可读性，指定了数值美元格式。

注意：由于下一个示例是查询且表未被更新，因此分配的属性仅在步骤持续时间内可用，并且不会永久保存在表的记录描述符中。

### SQL Code

```
PROC SQL;
    SELECT prodname, prodcost,
        .075 * prodcost FORMAT=DOLLAR7.2
            LABEL='Sales Tax'
    FROM PRODUCTS;
QUIT;
```

### Results

**The SAS System**

| Product Name | Product Cost | Sales Tax |
|---|---|---|
| Dream Machine | $3,200.00 | $240.00 |
| Business Machine | $3,300.00 | $247.50 |
| Travel Laptop | $3,400.00 | $255.00 |
| Analog Cell Phone | $35.00 | $2.63 |
| Digital Cell Phone | $175.00 | $13.13 |
| Office Phone | $130.00 | $9.75 |
| Spreadsheet Software | $299.00 | $22.43 |
| Database Software | $399.00 | $29.93 |
| Wordprocessor Software | $299.00 | $22.43 |
| Graphics Software | $299.00 | $22.43 |

## Ordering Output by Columns

按定义，表是无序的数据集。从表中获取的数据不会自动以任何特定顺序出现。为了抵消这种行为，SQL 过程提供了使用 `ORDER BY` 子句对表施加顺序的能力。当使用时，此子句根据一个或多个所选列中的值对查询结果进行排序；它必须在 `FROM` 子句之后指定。

数据行可以按升序（默认顺序）或降序（`DESC`）为每个指定的列排序（升序为默认顺序）。为了说明如何对所选列数据进行排序，让我们首先查看 `PRODUCTS` 表及其所有列按产品编号（`PRODNUM`）升序排列。

### SQL Code

```
PROC SQL;
    SELECT *
        FROM PRODUCTS
        ORDER BY prodnum;
QUIT;
```

### Results

**The SAS System**

| Product Name | Product Cost | Sales_Tax |
|---|---|---|
| Analog Cell Phone | $35.00 | 2.625 |
| Office Phone | $130.00 | 9.75 |
| Digital Cell Phone | $175.00 | 13.125 |
| Spreadsheet Software | $299.00 | 22.425 |
| Graphics Software | $299.00 | 22.425 |
| Wordprocessor Software | $299.00 | 22.425 |
| Database Software | $399.00 | 29.925 |
| Dream Machine | $3,200.00 | 240 |
| Business Machine | $3,300.00 | 247.5 |
| Travel Laptop | $3,400.00 | 255 |

The next example illustrates a query that selects and orders multiple columns of data from the `PRODUCTS` table. Output is arranged first in ascending order by product type (`PRODTYPE`) and then within product type in descending order by product cost (`PRODCOST`). The code and output are shown.

### SQL Code

```
PROC SQL;
    SELECT prodname, prodtype, prodcost, prodnum
    FROM PRODUCTS
    ORDER BY prodtype, prodcost DESC;
QUIT;
```

### Results

| Product Name | Product Type | Product Cost | Product Number |
|---|---|---|---:|---:|
| Travel Laptop | Laptop | $3,400.00 | 1700 |
| Digital Cell Phone | Phone | $175.00 | 2102 |
| Office Phone | Phone | $130.00 | 2200 |
| Analog Cell Phone | Phone | $35.00 | 2101 |
| Database Software | Software | $399.00 | 5002 |
| Spreadsheet Software | Software | $299.00 | 5001 |
| Graphics Software | Software | $299.00 | 5004 |
| Wordprocessor Software | Software | $299.00 | 5003 |
| Business Machine | Workstation | $3,300.00 | 1200 |
| Dream Machine | Workstation | $3,200.00 | 1110 |

## Grouping Data with Summary Functions

Occasionally it may be useful to display data in designated groups. A `GROUP BY` clause is used in these situations to aggregate and order groups of data using a designated column with the same value. When a `GROUP BY` clause is used without a summary function, SAS issues a warning in the SAS log with the message, “A `GROUP BY` clause has been transformed into an `ORDER BY` clause because neither the `SELECT` clause nor the optional `HAVING` clause of the associated table-expression referenced a summary function.” The `GROUP BY` clause is transformed into an `ORDER BY` clause and then processed.

When a `GROUP BY` clause is used without specifying a summary function in the `SELECT` statement, the entire table is treated as a single group and is ordered in ascending order. The next example illustrates a `GROUP BY` clause without any summary function specifications. Due to the absence of any summary functions, the `GROUP BY` clause is automatically transformed into an `ORDER BY` clause, with the rows being ordered in ascending order by product type (`PRODTYPE`).

### SQL Code

```
PROC SQL;
    SELECT prodtype,
        prodcost
    FROM PRODUCTS
        GROUP BY prodtype;
QUIT;
```

### Log Results

```
PROC SQL;
    SELECT prodtype,
        prodcost
    FROM PRODUCTS
        GROUP BY prodtype;
WARNING: A GROUP BY clause has been transformed into an ORDER BY clause because neither the SELECT clause nor the optional HAVING clause of the associated table-expression referenced a summary function.
QUIT;
```

### Results

![](img/9d3e4d8fa063e50a0c9985e34cf9d6e8_130_0.png)

When a `GROUP BY` clause is used with a summary function, the rows are aggregated in a series of groups. This means that an aggregate function is evaluated on a group of rows and not on a single row at a time. Suppose that the least expensive product in each product type category (`PRODTYPE`) needs to be identified. A separate query for each product category could be specified using the `MIN` function to determine the cheapest product. But this would require separate runs to be executed—not a very good approach. A better way to do this would be to specify a `GROUP BY` clause in a single statement as follows.

### SQL Code

```
PROC SQL;
    SELECT prodtype,
           MIN(prodcost) AS Cheapest
           format=dollar9.2 label='Least Expensive'
    FROM PRODUCTS
         GROUP BY prodtype;
QUIT;
```

### Results

| Product Type | Least Expensive |
|---|---:|
| Laptop | $3,400.00 |
| Phone | $35.00 |
| Software | $299.00 |
| Workstation | $3,200.00 |

## Grouping Data and Sorting

In the absence of an `ORDER BY` clause, the SQL procedure automatically sorts the results from a grouped query in the same order as specified in the `GROUP BY` clause. When both an `ORDER BY` clause and `GROUP BY` clause are specified for the same column(s) or column order, no additional processing occurs to satisfy the request. Because the `ORDER BY` clause and `GROUP BY` clause are not mutually exclusive, they can be used together. Internally, the `GROUP BY` clause first sorts the results on the grouping column(s) and then aggregates the rows of the query by the same grouping column.

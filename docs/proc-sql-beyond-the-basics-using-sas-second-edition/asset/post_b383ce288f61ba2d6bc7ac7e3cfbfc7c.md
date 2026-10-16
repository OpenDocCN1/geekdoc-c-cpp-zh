
## Specifying a WHERE Clause

To provide greater subsetting capabilities as well as added flexibility, the SQL procedure also permits the specification of an optional WHERE clause in addition to an ON clause when constructing outer joins. The ability to specify a WHERE clause in conjunction with an ON clause permits greater control over the subsetting of rows. An example will help illustrate how a WHERE clause is used in an outer join. Suppose that you want to limit the results from the previous left outer join to only those products that cost less than $300.00. In this example, the left outer join syntax uses a WHERE clause to subset row results to nonmissing products that cost less than $300.00.

### SQL Code

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

The optional WHERE clause that is specified in addition to an ON clause in an outer join further subsets the joined results.

### Results

| Manufacturer Name | Manufacturer City | Manufacturer Number | Product Type | Product Cost |
|---|---|---|---|---|
| Global Comm Corp | San Diego | 210 | Phone | $175.00 |
| Global Comm Corp | San Diego | 210 | Phone | $35.00 |
| KPL Enterprises | San Diego | 500 | Software | $299.00 |
| KPL Enterprises | San Diego | 500 | Software | $299.00 |
| KPL Enterprises | San Diego | 500 | Software | $299.00 |

## Specifying Aggregate Functions

Suppose that you need to produce a monthly report that consists of a total invoice amount by manufacturer. An aggregate function can be specified with outer join syntax to perform a group computation using a GROUP BY clause. In the next example, a left join computes the total invoice amount for each manufacturer with a SUM function and GROUP BY clause.

### SQL Code

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

- The SUM function computes the total invoice amount for each manufacturer.
- The GROUP BY clause groups all of the rows associated with a manufacturer into a single row.

The results show that manufacturers with no activity have a null or missing value in the aggregated Total_Invoice_Amt column.

### Results

| Manufacturer Name | Total_Invoice_Amt |
|---|---|
| Cupid Computer | $9,600.00 |
| Global Comm Corp | $245.00 |
| KPL Enterprises | $25,789.00 |
| San Diego PC Planet | . |
| Storage Devices Inc | . |
| World Internet Corp | $1,598.00 |

## Right Outer Joins

Right joins are similar to left joins, except that the rows in the right (second) table are preserved. Consequently, the results contain the rows of the symmetric join plus a row for each unmatched row in the right table. Nulls are automatically substituted for values from the left table. Suppose that you want to see all manufacturers and their respective products. In the next example, a simple report that contains products, product type, manufacturer number, and manufacturer name is produced from the PRODUCTS and MANUFACTURERS tables using a right outer join construct.

### SQL Code

```
PROC SQL;
    SELECT prodname, prodtype,
        products.manunum, manuname
    FROM PRODUCTS RIGHT JOIN MANUFACTURERS
        ON products.manunum = manufacturers.manunum;
QUIT;
```

- The RIGHT JOIN specification preserves all of the rows in the right table (MANUFACTURERS) even when there are no matching rows in the left table (PRODUCTS).

The results show that manufacturers that appear in the MANUFACTURERS table with no products listed in the PRODUCTS table have null or missing values in the Product Name, Product Type, and Manufacturer Number columns.

Note: To remove rows with missing values in the results, a WHERE clause could be specified.

### Results

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

## Full Outer Joins

Full outer joins combine the power of left and right joins by preserving rows from both the left and right tables. Although a full join is not used as frequently as left join or right join constructs, it can be useful when information from both tables is missing. In the next example, a full outer join is specified to produce a report that contains manufacturers with no products and products with no known manufacturers.

### SQL Code

```
PROC SQL;
    SELECT prodname, prodtype,
        products.manunum, manuname
    FROM PRODUCTS FULL JOIN MANUFACTURERS
        ON products.manunum =
            manufacturers.manunum;
QUIT;
```

- The full join specification preserves all of the rows in the left table (PRODUCTS) as well as all of the rows in the right table (MANUFACTURERS) even when there are no matching rows.

### Results

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

## Subqueries

Now that you have seen how two or more tables can be combined in a join query, turn your attention to another type of complex query known as a subquery. A subquery is a query expression that is nested within another query expression. Its purpose is to have the inner query produce a single value or multiple values that can then be passed into the outer query for processing. You achieve this by embedding a SELECT statement inside a WHERE clause of an outer query’s SELECT statement, INSERT statement, DELETE statement, or HAVING clause.

Note: You should avoid nesting more than two subqueries deep because of the conceptual and processing complexities this introduces.

The typical subquery consists of a (inner) query combined inside the predicate of another (outer or main) query. When processed, the inner query passes a Boolean value to the outer query consisting of either True if it returns a minimum of one row or False if no rows are returned by the subquery. The results of the inner query are stored in a temporary results table and used as input to the main query. Our exploration of subqueries will involve using them with comparison operators, the IN predicate, and the ANY and ALL keywords, and will conclude with a look at a special type of subquery called a correlated subquery.

## Alternate Approaches to Subqueries

A subquery is a very useful construct, especially when information from multiple tables needs to be interrelated. Unfortunately, a subquery is not always easy to construct and might be even more difficult to understand. So before constructing every table relation with a subquery, consider your options carefully.

When all of the information is available in a single table, a simple query is probably all that needs to be constructed. Suppose that you want to produce a report that consists of the invoice information for Global Comm Corp. Let’s further assume that you know the specific manufacturer number for Global Comm Corp. Knowing this means that you don’t have to go into the MANUFACTURERS table to find it. In the next example, a simple query is constructed to retrieve all of the invoice information from the INVOICE table.

### Simple Query

```
PROC SQL;
    SELECT *
        FROM INVOICE
        WHERE manunum = 210;
QUIT;
```

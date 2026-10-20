
## How to sort the results of a query

If you want the results of a query to be returned in a particular sequence, you can include the orderby clause in the query expression. The syntax of this clause is shown at the top of figure 18-5. This syntax indicates that you can sort by one or more expressions in either ascending or descending sequence.

To understand how this works, the first example in this figure shows how you might sort the salesTotals array. Here, the query expression includes an orderby clause that sorts the elements in this array in ascending sequence (the default). To do that, it names the range variable that is declared by the from clause. If you compare the results of this query with the results shown in the previous figure, you’ll see how the sequence has changed.

The second example shows how you can sort query results by two expressions. In this case, the query will return invoices from the generic invoice list in descending invoice total sequence within customer ID sequence. If you look at the results of this query, you can see that the customer IDs are in ascending sequence. You can also see that the second and third invoices are for the same customer, and the invoice with the largest total is listed first.

### The syntax of the orderby clause

```
orderby expression1 [ascending|descending]
    [, expression2 [ascending|descending]]...
```

### An example that sorts the salesTotals array

### A query expression that sorts the sales in ascending sequence

```
var salesList = from sales in salesTotals
    where sales > 2000
    orderby sales
    select sales;
```

### Code that executes the query

```
string salesDisplay = "";
foreach (var sales in salesList)
    salesDisplay += sales.ToString("c") + "\t\t\t\n";
MessageBox.Show(salesDisplay, "Sorted Sales Over $2000");
```

![](img/844f608d10a44654833ea5efc8a2e7a7_613_0.png)

### An example that sorts the generic list of invoices

### A query expression that sorts the invoices by customer ID and invoice total

```
var invoices = from invoice in invoiceList
    where invoice.InvoiceTotal > 150
    orderby invoice.CustomerID, invoice.InvoiceTotal descending
    select invoice;
```

### Code that executes the query

```
string invoiceDisplay = "Cust ID\tInvoice amount\n";
foreach (var invoice in invoices)
    invoiceDisplay += invoice.CustomerID + "\t"
        + invoice.InvoiceTotal.ToString("c") + "\n";
MessageBox.Show(invoiceDisplay, "Sorted Invoices Over $150");
```

![](img/844f608d10a44654833ea5efc8a2e7a7_613_1.png)

### Description

- The orderby clause lets you specify how the results of the query are sorted. You can specify one or more expressions on this clause.

Figure 18-5    How to sort the results of a query

## How to select fields from a query

So far, the queries you’ve seen in this chapter have returned entire elements of a data source. To do that, the select clause simply named the range variable that represents those elements. But you can also return selected fields of the elements. To do that, you code the select clause as shown in figure 18-6. As you can see, the select clause lets you identify one or more fields to be included in the query results. A query that returns something other than entire source elements is called a projection.

To illustrate how this works, the first example in this figure uses a sorted list named employeeSales. The keys for this list are employee names, and the values are sales totals. You can see the definition of this list and the data it contains at the beginning of this example.

The query expression that uses this list includes the from, where, and orderby clauses. The where clause indicates that only those elements with values (sales totals) greater than 2000 should be returned, and the orderby clause indicates that the returned elements should be sorted by the values in descending sequence. In addition, this query expression includes a select clause that indicates that only the key field (the employee name) should be returned.

The foreach statement that executes this query works like the others you’ve seen in this chapter. It creates a string that includes a list of the employee names. Notice, however, that the name of the iteration variable that’s used in this statement is different from the name of the range variable used in the query expression. That’s because the variable in the query expression refers to an element in the sorted list, but the variable in the foreach statement refers only to the employee names returned from the list by the query.

The second example shows a query expression that returns selected fields from the Invoice objects. Specifically, it returns the CustomerID and InvoiceTotal fields. If you look back at the example in the previous figure, you’ll see that these are the only two fields that are used when the query is executed. Because of that, these are the only two fields that need to be retrieved.

Notice that the select clause in this example uses an object initializer to create the objects that are returned by the query. In this case, each object includes a CustomerID property and an InvoiceTotal property. Unlike the object initializers you saw in chapter 12, however, the object initializer shown here doesn’t specify a type. That’s because a type that includes just CustomerID and InvoiceTotal properties doesn’t exist. In that case, an anonymous type is created. Note that because the name of an anonymous type is generated by the compiler, you can’t refer to it directly. In most cases, that’s not a problem. If it is, you can define the type you want to use and then name it on the object initializer.

In addition to the type, the names of the properties have been omitted from the object initializer. Because of that, the properties are given the same names as the fields that are listed in the initializer. If that’s not what you want, you can specify the names in the initializer. For example, if you wanted to name the two properties of the type shown here ID and Total, you would code the initializer like this:

```
new { ID = invoice.CustomerID, Total = invoice.InvoiceTotal }
```

### Two ways to code the select clause

```
select columnExpression
select new [type] { [PropertyName1 =] columnExpression1
[, [PropertyName2 =] columnExpression2]... }
```

### An example that selects key values from a sorted list

### The employee sales sorted list

```
SortedList<string, decimal> employeeSales = new SortedList<string, decimal>
{ ["Anderson"] = 1286.45m, ["Menendez"] = 2433.49m,
["Thompson"] = 2893.85m, ["Wilkinson"] = 2094.53m };
```

### A query expression that selects the employee names from the list

```
var employeeList = from sales in employeeSales
where sales.Value > 2000
orderby sales.Value descending
select sales.Key;
```

### Code that executes the query

```
string employeeDisplay = "";
foreach (var employee in employeeList)
    employeeDisplay += employee + "\t\t\t\n";
MessageBox.Show(employeeDisplay, "Sorted Employees With Sales Over $2000");
```

![](img/844f608d10a44654833ea5efc8a2e7a7_615_0.png)

### A query expression that creates an anonymous type from the list of invoices

```
var invoices = from invoice in invoiceList
where invoice.InvoiceTotal > 150
orderby invoice.CustomerID, invoice.InvoiceTotal descending
select new { invoice.CustomerID, invoice.InvoiceTotal };
```

### Description

- The *select* clause indicates the data you want to return from each element of the query results.
- A query that returns anything other than entire source elements is called a *projection*. Both examples above illustrate projections.
- To return two or more fields from each element, you code an object initializer within the select clause. If the object initializer doesn’t specify a type, an *anonymous type* that contains the specified fields as its properties is created.

## How to join data from two or more data sources

Figure 18-7 shows how you can include data from two or more data sources in a query. To do that, you use the join clause shown at the top of this figure. To start, this clause declares a range variable and names a data source just like the from clause does. Then, it indicates how the two data sources are related.

To illustrate, the example in this figure joins data from the list of Invoice objects you’ve seen in the previous figures with a list of Customer objects. You can see the definition of the Customer class at the beginning of this example, along with the statements that declare and load the two lists. Like the invoice list, the customer list is loaded by calling a method of a database class.

The query expression that follows joins the data in these two lists. To do that, it names the invoice list on the from clause, and it names the customer list on the join clause. Then, the on condition indicates that only customers in the customer list with customer IDs that match customer IDs in the invoice list should be included in the results.

Because both the invoice and customer lists are included as data sources in this query expression, the rest of the query can refer to fields in either data source. For example, the orderby clause in this query expression sorts the results by the InvoiceTotal field in the invoice list within the Name field in the customer list. Similarly, the select clause selects the Name field from the customer list and the InvoiceTotal field from the invoice list.

The remaining code in this example executes the query and creates a list that includes the customer names and invoice totals. This is similar to the list you saw in figure 18-5. Because the list in figure 18-7 includes the customer names instead of the customer IDs, however, it provides more useful information.

Although this figure only shows how to join data from two data sources, you can extend this syntax to join data from additional data sources. For example, suppose you have three data sources named invoiceList, lineItemList, and productList. Then, you could join the data in these lists using code like this:

```
from invoice in invoiceList
join lineItem in lineItemList
    on invoice.InvoiceID equals lineItem.InvoiceID
join product in productList
    on lineItem.ProductCode equals product.ProductCode
```

Once the three tables are joined, you can refer to fields from any of these tables in the query expression.

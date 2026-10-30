
## NOTE

A Yes/No field can have three states: Yes, No, and Null. Null occurs only when no default value was set in a table and the value has not yet been entered. Checking for Is Null displays only records containing Null in the field, and checking for Is Not Null always displays all records with Yes or No in the field. After a Yes/No field check box is checked (or checked and then deselected), it can never be Null. It must be either Yes or No (-1 or 0).

## Entering OLE object criteria

You can specify criteria for OLE objects: Is Null or Is Not Null. For example, suppose you don't have pictures for all the products and you want to view only those records that have a picture—that is, those in which the picture is not null. You specify the Is Not Null criterion for the Picture field of tblProducts.

## Tip

Although Is Not Null is the correct syntax, you can also use Not Null in the QBE grid, and Access supplies the Is operator for you.

## Using Multiple Criteria in a Query

In previous sections of this chapter, you worked with single-condition criteria on a single field. As you learned in those sections, you can specify single-condition criteria for any field type. In this section, you work with multiple criteria based on a single field. For example, you might be interested in seeing all records in which the buyer comes from New York, California, or Arizona. Or maybe you want to view the records of all the products sold during the first quarter of the year 2012.

The QBE pane has the flexibility to solve these types of problems. You can specify criteria for several fields in a select query. Using multiple criteria, for example, you can determine which products were sold for the past 90 days. Either of the following expressions could be used as criteria in the SaleDate field's criteria:

```
Between Date() And Date() - 90
Between Date() And DateAdd("d",-90,Date())
```

Of these, the expression using the DateAdd function is less ambiguous and more specific to the task.

We delve deeper into the topic of creating calculations with dates in Chapter 12.

## Understanding an Or operation

You use an Or operator in queries when you want a field to meet either of two conditions. For example, you might want to see all the records where the customer has an address in

### Using the Or cell of the QBD pane

Besides using the literal Or operator as a single expression on the Criteria row under the State field, you can supply individual criteria for the field vertically on separate rows of the QBD pane, as shown in Figure 9.11.

> **TIP**
> 
> Access allows up to nine Or cells for each field. If you need to specify more Or conditions, use the Or operator between conditions (for example, AZ Or CA Or NY Or PA).

Access rearranges the design shown in Figure 9.11 when the query is saved to match the query in Figure 9.10. In fact, when you open the Figure-11 query in the Chapter09.accdb example database, you’ll see that it is exactly the same as the Figure-10 query because of the way Access rearranged the criteria when the Figure-11 query was originally saved. When you build a query using “vertical” Or criteria, Access optimizes the SQL statement behind the query by placing all the Or criteria into a single expression.

**FIGURE 9.11**

Using the Or cell of the QBD pane. You can place criteria vertically in the QBD grid.

![](img/1e45673ab6eca9d20e67635ff5b9b318_342_0.png)

### Using a list of values with the In operator

Another method for specifying multiple values of a single field is using the In operator. The In operator finds a value from a list of values. For example, use the expression In (AZ, CA, NY) under the State field in the query used in Figure 9.11. The list of values in the parentheses becomes an example criterion. Your query should resemble the query shown in Figure 9.12.

Access automatically adds quotation marks around AZ, CA, and NY.

**FIGURE 9.12**

Using the In operator to find all records for buyer state being either AZ, CA, or NY.

![](img/1e45673ab6eca9d20e67635ff5b9b318_343_0.png)

## NOTE

When you work with the In operator, each value (example data) must be separated from the others by a comma.

## Using And to specify a range

The And operator is frequently used in fields that have numeric or date/time data types. It's seldom used with text data types, although it can be this way in some situations. For example, you might be interested in viewing all buyers whose names start with the letters d, e, or f. The And operator can be used here (>="D" And <="G"), although the Like operator is better (Like "[DEF] *") because it's much easier to understand.

You use the And operator in queries when you want a field to meet two or more conditions that you specify. For example, you might want to see records of buyers who have purchased products between October 1, 2012, and March 31, 2013. In other words, the sale had to have occurred during the last quarter of the year 2012 and the first quarter of 2013. The general expression for this example is:

```
(SaleDate >= #10/1/2012#) And (SaleDate <= #3/31/2013#)
```

## NOTE

Parentheses are included in this example for clarity.

Unlike the Or operation (which has several conditions under which it is true), the And operation is true only when both sides of the expression are true. To clarify the use of the And operator, consider these conditions:

- `SaleDate (9/22/2012)` is not greater than `10/01/2012` but is less than `3/31/2013`: The result is false.
- `SaleDate (4/11/2013)` is greater than `10/01/2012` but is not less than `3/31/2013`: The result is false.
- `SaleDate (11/22/2012)` is greater than `10/01/2012` and less than `3/31/2013`: The result is true.

Using an And operator with a single field sets a range of acceptable values in the field. Therefore, the key purpose of an And operator in a single field is to define a range of records to be viewed. For example, you can use the And operator to create a range criterion to display all viewers who have purchased products between October 1, 2012 and March 31, 2013, inclusively. To create this query, follow these steps:

- 1. **Create a new query using tblCustomers and tblSales.**
- 2. **Add Company from tblCustomers and SaleDate from tblSales.**
- 3. **Click in the Criteria cell of SaleDate.**
- 4. **Type `>= #10/1/2012# And <= #3/31/2013#` in the cell.** The query should resemble Figure 9.13.

**FIGURE 9.13**

Using an And operator to specify complex query criteria.

![](img/1e45673ab6eca9d20e67635ff5b9b318_344_0.png)

Notice the pound signs (#) used to delimit the dates in the expressions on both sides of the And operator. Access recognizes pound signs as delimiters for date and time values.

Without the pound signs, Access evaluates the date values as numeric expressions (10 divided by 1 divided by 2012, for example).

## Using the Between...And operator

You can request a range of records using another method—the Between...And operator. With Between...And, you can find records that meet a range of values—for example, all sales where the list price of the product was between $50 and $100. Using the previous example with dates, create the query shown in Figure 9.14.

**FIGURE 9.14**

Using the Between...And operator. The results are the same as the query in Figure 9.13.

![](img/1e45673ab6eca9d20e67635ff5b9b318_345_0.png)

The operands for the Between...And operator are inclusive. This means that sales on 10/1/2012 and 3/31/2013 are included in the query results.

## Searching for null data

A field might have no contents for several reasons. For example, perhaps the value wasn’t known at the time of data entry, or the person who did the data entry simply forgot to enter the information, or the field’s information was removed. Access does nothing with this field. Unless a default value is specified in the table design, the field simply remains empty. (A field is said to be null when it’s truly empty.)

Logically, null is neither true nor false. A null field is not equivalent to all spaces or to zero. A null field simply has no value.

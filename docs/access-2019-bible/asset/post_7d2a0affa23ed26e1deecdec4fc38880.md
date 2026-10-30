
# FIGURE 10.21

In this query, you are updating the zip code for all customers that have a code of 33605 to 33606.

![](img/1e45673ab6eca9d20e67635ff5b9b318_377_0.png)

# FIGURE 10.22

Click Yes to continue with your update action.

![](img/1e45673ab6eca9d20e67635ff5b9b318_377_1.png)

## Using Expressions in Your Update Queries

You'll come across situations in which you have to execute record-specific updates. That is, you aren't updating multiple records with one specific value; instead, you're updating each record individually based on an expression.

To demonstrate this concept, start a query in Design view based on the SalesHistory table you created in the "Make-table queries" section earlier in this chapter. Build your query like the one shown in the following figure.

![](img/1e45673ab6eca9d20e67635ff5b9b318_378_0.png)

This query is telling Access to update the Period to the concatenated text “PD” with the value in the Period field.

After you run this query, all the values in the Period field will have a prefix of PD. For example, 201201 will be updated to PD201201.

Remember: This is just one example of an expression you can use to update your records. You can use almost any expression with an update query, ranging from mathematical functions to string operations.

## A Word on Updatable Data Sets

Not all data sets are updatable. That is, you may have a data set that Access can’t update for one reason or another. If your update query fails, you’ll get one of these messages: Operation must use an updatable query or This recordset is not updatable.

Your update query will fail if any one of the following applies:

- Your query is using a join to another query. To work around this issue, create a temporary table that you can use instead of the joined query.
- Your query is based on a crosstab query, an aggregate query, a union query, or a subquery that contains aggregate functions. To work around this issue, create a temporary table that you can use instead of the query.
- Your query is based on three or more tables and there is a many-to-one-to-many relationship. To work around this issue, create a temporary table that you can use without the relationship.
- Your query is based on a table where the Unique Values property is set to Yes. To work around this issue, set the Unique Values property of the table to No.
- Your query is based on a table that's locked by another user. To work around this issue, ensure the table is not in Design view or locked by another user.
- Your query is based on a table in a database that is open as read-only or is located on a read-only drive. To work around this issue, obtain write access to the database or drive.
- Your query is based on a linked ODBC table with no unique index or a paradox table without a primary key. To work around this issue, add a primary key or a unique index to the linked table.
- Your query is based on a SQL pass-through query. To work around this issue, create a temporary table that you can use instead of the query.

## Crosstab Queries

A crosstab query is a special kind of aggregate query that summarizes values from a specified field and groups them in a matrix layout by two sets of dimensions, one set down the left side of the matrix and the other set listed across the top of the matrix. Crosstab queries are perfect for analyzing trends over time or providing a method for quickly identifying anomalies in your data set.

The anatomy of a crosstab query is simple. You need a minimum of three fields in order to create the matrix structure that will become your crosstab. The first field makes up the row headings; the second field makes up the column headings; and the third field makes up the aggregated data in the center of the matrix. The data in the center can represent a Sum, Count, Average, or any other aggregate function. Figure 10.23 demonstrates the basic structure of a crosstab query.

# FIGURE 10.23

The basic structure of a crosstab query.

| Region Name | QTR1 | QTR2 | QTR3 | QTR4 |
|-------------|------|------|------|------|
| Region A    | data | data | data | data |
| Region B    | data | data | data | data |
| Region C    | data | data | data | data |

There are two methods to create a crosstab query. You can use the Crosstab Query Wizard or create a crosstab query manually using the query design grid.

## Creating a crosstab query using the Crosstab Query Wizard

To use the Crosstab Query Wizard to create a crosstab query, follow these steps:

- 1. Select the Create tab of the Ribbon and then click the Query Wizard button.
  The New Query dialog box, shown in Figure 10.24, appears.

# FIGURE 10.24

Select Crosstab Query Wizard from the New Query dialog box.

![](img/1e45673ab6eca9d20e67635ff5b9b318_380_0.png)

- 2. **Select Crosstab Query Wizard from the selection list, and then click OK.**
  
  The first step in the Crosstab Query Wizard is to identify the data source you’ll be using. As you can see in Figure 10.25, you can choose either a query or a table as your data source. In this example, you’ll be using the Dim_Transactions table as your data source.
  
- 3. **Select Dim_Transactions and then click the Next button.**
  
  The next step is to identify the fields you want to use as the row headings.
  
- 4. **Select the ProductID field and click the button with the > symbol on it to move it to the Selected Fields list.** The dialog box should look like Figure 10.26. Notice that the ProductID field is shown in the sample diagram at the bottom of the dialog box. You can select up to three fields to include in your crosstab query as row headings. Remember that Access treats each combination of headings as a unique item. That is, each combination is grouped before the records in each group are aggregated.
  
- 5. **Click the Next button.**
  
  The next step is to identify the field you want to use as the column heading for your crosstab query. Keep in mind that there can be only one column heading in your crosstab query.
  
- 6. **Select the OrderDate field from the field list.** Notice in Figure 10.27 that the sample diagram at the bottom of the dialog box updates to show the OrderDate.

> **NOTE**
> 
> If the field that is being used as a column heading includes data that contains a period (.), an exclamation point (!), or a bracket ([ or ]), those characters will be changed to an underscore character (_) in the column heading. This does not happen if the same data is used as a row heading. This behavior is by design, as the naming convention for field names in Access prohibits use of these characters.

# FIGURE 10.25

Select the data source for your crosstab query.

![](img/1e45673ab6eca9d20e67635ff5b9b318_381_0.png)

# FIGURE 10.26

Select the ProductID field and then click the Next button.

![](img/1e45673ab6eca9d20e67635ff5b9b318_381_1.png)

## 1.1 认识三角形

由不在同一条直线上的三条线段首尾顺次相接所组成的图形叫做三角形。

三角形可以用符号"△"表示，顶点是A、B、C的三角形，记作"△ABC"，读作"三角形ABC"。

△ABC的三边，有时也用a、b、c来表示。如图1-2，顶点A所对的边BC用a表示，顶点B所对的边AC用b表示，顶点C所对的边AB用c表示。

![](img/1e45673ab6eca9d20e67635ff5b9b318_382_0.png)

图1-2

三角形有三个内角，三个顶点，三条边。

在三角形中，角平分线、中线、高线都是三角形中的重要线段。

每个三角形都有三条角平分线、三条中线、三条高线，它们分别交于一点。

10. In this case, you want to view your query results so simply click the Finish button.

In just a few clicks, you’ve created a powerful look at the revenue performance of each product by quarter (see Figure 10.31).

# FIGURE 10.30

Click Finish to see your query results.

![](img/1e45673ab6eca9d20e67635ff5b9b318_384_0.png)

# FIGURE 10.31

A powerful analysis in just a few clicks.

| Product ID | Total of LineTotal | Qtr 1 | Qtr 2 | Qtr 3 | Qtr 4 |
|---|---:|---:|---:|---:|---:|
| 709 | $28,663.80 | $3,787.20 | $8,000.40 | $9,485.40 | $7,390.80 |
| 710 | $353,507.05 | $69,334.85 | $64,463.10 | $82,670.60 | $136,858.50 |
| 718 | $732,725.50 | — | $71,432.25 | $54,166.75 | $147,126.50 |
| 719 | $5,853,748.80 | $1,244,884.20 | $1,541,942.70 | $1,616,661.00 | $1,450,260.90 |
| 720 | $495,413.50 | — | — | $495,413.50 | — |
| 732 | $160,733.00 | $23,115.00 | $49,948.50 | $36,247.00 | $51,422.50 |
| 733 | $57,352.00 | — | $22,411.50 | $13,065.00 | $21,875.50 |
| 753 | $3,973,695.50 | $2,286,041.00 | $2,949,132.00 | $1,824,659.50 | $2,313,863.00 |
| 755 | $582,601.20 | $145,650.30 | $166,482.60 | $103,370.40 | $167,097.90 |
| 756 | $206,095.35 | $133,975.85 | $155,210.75 | $85,507.75 | $51,401.00 |
| 757 | $250,742.10 | $82,378.10 | $83,924.30 | $124,890.65 | — |
| 759 | $517,812.55 | $116,694.85 | $147,762.65 | $124,890.65 | $128,464.40 |
| 760 | $1,680,850.20 | $340,321.65 | $439,951.80 | $489,024.00 | $411,552.75 |
| 761 | $1,609,727.40 | $346,173.30 | $433,207.60 | $433,159.70 | $397,186.80 |
| 762 | $1,970,584.00 | $412,384.00 | $521,899.00 | $558,061.00 | $478,240.00 |
| 763 | $1,381,724.40 | $298,040.80 | $374,013.60 | $373,272.00 | $336,398.00 |

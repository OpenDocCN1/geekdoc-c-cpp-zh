
2. Type CARS into the Criteria cell under the Category column (see Figure 8.15). Notice that Access adds double quotes around the value. Unlike many other database systems, Access automatically makes assumptions about what you want.

3. Run the query. Note that only cars are displayed in the query's results.

## FIGURE 8.15

Specifying Cars as the query's criteria.

![](img/1e45673ab6eca9d20e67635ff5b9b318_296_0.png)

When looking at the results of the query, you may argue that there is no point in displaying Cars in every row. In fact, because this query only returns information about cars, the user can assume that every record references a car, and there's no need to display a product category in the query. Unchecking the Category field's Show box in the query's design removes Category from the datasheet, making the data easier to understand.

You could enter the criteria expression in any of these other ways:

- CARS
- = CARS
- "CARS"
- = "Cars"

By default, Access is not case sensitive, so any form of the word cars works just as well as this query's criteria.

Figure 8.15 is an excellent example for demonstrating the options for various types of simple character criteria. You could just as well enter Not Cars in the criteria for the column to return all products that are not cars (trucks, vans, and so on).

Generally, when dealing with character data, you enter equalities, inequalities, or a list of acceptable values.

This capability is a powerful tool. Consider that you only have to supply an example, and Access not only interprets it but also uses it to create the query recordset. This is exactly what Query by Example means: you enter an example and let the database build a query based on the example.

To erase the criteria in the cell, select the contents and press Delete, or select the contents and right-click Cut from the shortcut menu that appears.

## Entering other simple criteria

You can also specify criteria for Numeric, Date, and Yes/No fields. Simply enter the example data in the criteria field just as you did for text fields. In almost every case, Access understands the criteria you enter and adjusts to correctly apply the criteria to the query's fields.

It's also possible to add more than one criteria to a query. For example, suppose that you want to look only at contacts who live in Connecticut and have been customers since January 1, 2010 (where OrigCustDate is greater than or equal to January 1, 2010). This query requires criteria in both the State and OrigCustDate fields. To do this, it's critical that you place both examples on the same criteria row. Follow these steps to create this query:

- 1. Create a new query starting with tblContacts.
- 2. Add OrigCustDate, LastName, FirstName, and State to the QBE grid.
- 3. Enter CT in the Criteria cell in the State column.
- 4. Enter >= 01/01/2010 in the Criteria cell in the OrigCustDate column. Access adds pound sign characters (#) around the date in the criteria box. Figure 8.16 shows how the query should look.
- 5. Run the query.

Access displays records of customers who live in Connecticut and who became customers after January 1, 2010.

Access uses comparison operators to compare Date fields to a value. These operators include less than (<), greater than (>), equal to (=), or a combination of these operators.

Notice that Access automatically adds pound sign (#) delimiters around the date value. Access uses these delimiters to distinguish between date and text data. The pound signs are just like the quote marks Access added to the "Cars" criteria. Because OrigCustDate is a DateTime field, Access understands what you want and inserts the proper delimiters for you.

## FIGURE 8.16

Specifying text and date criteria in the same query.

![](img/1e45673ab6eca9d20e67635ff5b9b318_298_0.png)

Be aware that Access interprets dates according to the region and language settings in the Windows Control Panel. For example, in most of Europe and Asia, #5/6/2010# is interpreted as June 5, 2010, while in the United States this date is May 6, 2010. It's very easy to construct a query that works perfectly but returns the wrong data because of subtle differences in regional settings.

We cover operators and precedence in more detail in Chapter 9.

## Printing a Query's Recordset

After you create your query, you can easily print all the records in the recordset. Although you can't specify a type of report, you can print a simple matrix-type report (rows and columns) of the recordset created by your query.

You do have some flexibility when printing a recordset. If you know that the datasheet is set up just as you want, you can specify some options as you follow these steps:

- 1. Run the query you just created for Connecticut customers who've been active since January 1, 2010.
- 2. Choose File ▸ Print. This will present you with three options: you can Quick Print without specifying any print settings, you can Print using specific print settings, or you can Print Preview to preview the output before printing. In this case, let's select the Print command.
- 3. Specify the print options that you want in the Print dialog box and click OK.

## Part III: Working with Access Queries

The printout reflects all layout options in effect when you print the recordset. Hidden columns don’t print, and gridlines print only if the Gridlines option is on. The printout reflects the specified row height and column width.

## Saving a Query

To save your query, click the Save button on the Quick Access toolbar at the top of the Access screen. Access asks you for the name of the query if this is the first time the query has been saved.

After saving the query, Access returns you to the mode you were working in. Occasionally, you’ll want to save and exit the query in a single operation. To do this, click the Close Window button in the upper-right corner of the Query Designer. Access always asks you to confirm saving the changes before it actually saves and closes the query.

## Creating Multi-table Queries

Using a query to get information from a single table is common; often, however, you need information from several related tables. For example, you might want to obtain a buyer’s name and product purchased by the customer. This query requires four tables: tblCustomers, tblSales, tblSalesLineItems, and tblProducts.

![](img/1e45673ab6eca9d20e67635ff5b9b318_299_0.png)

> In Chapter 4, you learned the importance of primary and foreign keys and how they link tables together. You learned how to use the Relationships window to create relationships between tables. Finally, you learned how referential integrity affects data in tables.

After you create the tables for your database and decide how the tables are related to one another, you’re ready to build multi-table queries to obtain information from several related tables. A multi-table query presents data as if it existed in one large table.

The first step in creating a multi-table query is to add the tables to the query design window:

- 1. Create a new query by clicking the Query Design button on the Create tab of the Ribbon.
- 2. Add tblCustomers, tblSales, tblSalesLineItems, and tblProducts by double-clicking each table’s name in the Show Table dialog box.
- 3. Click the Close button.

> **NOTE**
> You can also add each table by highlighting the table in the list separately and clicking Add.

## Figure 8.17 shows the top pane of the query design window (the section in gray) with the four tables you just added. Because the relationships were set at table level, the join lines are automatically added to the query.

## FIGURE 8.17

![](img/1e45673ab6eca9d20e67635ff5b9b318_300_0.png)

> **NOTE**
> 
> You can add more tables at any time by choosing Show Table from the Query Tools Design Ribbon. Alternatively, you can right-click the design window and select the Show Table option from the shortcut menu.

You add fields from more than one table to the query in exactly the same way as you do when you’re working with a single table. You can add fields one at a time, multiple fields as a group, or all the fields from a table.

When you select a field that has a common name in multiple tables, Access adds the table’s name, followed by a period and the field name. For example, if ProductID is a field found in more than one table used in the query design window (let’s say tblProducts and tblSales-LineItems), adding the ProductID field from tblSalesLineItems will display that field in the design grid as tblSalesLineItems.ProductID. This helps you select the correct field name. Using this method, you can select a common field name from a specific table.

> **TIP**
> 
> The easiest way to select fields is still to double-click the field names in the top pane of the Query Designer. To do so, you might have to resize the field list windows to see all the fields you want to select.

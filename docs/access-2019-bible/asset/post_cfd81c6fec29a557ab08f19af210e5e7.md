
## Using fields in calculations

Not all your calculations will require you to specify a constant. In fact, many of the mathematical operations you'll carry out will be performed on data that already resides in fields within your data set. You can perform calculations using any fields formatted as number or currency.

For instance, in the query shown in Figure 12.2, you aren't using any constants. Instead, your calculation will be executed using the values in each record of the data set. This is similar to referencing cell values in an Excel formula.

## FIGURE 12.2

In this query, you're using two fields in a Dollar Variance calculation.

![](img/1e45673ab6eca9d20e67635ff5b9b318_424_0.png)

## Using the results of aggregation in calculations

Using the result of an aggregation as an expression in a calculation allows you to perform multiple analytical steps in one query. In the example in Figure 12.3, you're running an aggregate query. This query will execute in the following order:

- 1. The query groups your records by market.
- 2. The query calculates the count of orders and the sum of revenue for each market.
- 3. The query assigns the aliases you've defined respectively (OrderCount and Rev).
- 4. The query uses the aggregation results for each branch as expressions in your AvgDollarPerOrder calculation.

## Using the results of one calculation as an expression in another

Keep in mind that you aren't limited to one calculation per query. In fact, you can use the results of one calculation as an expression in another calculation. Figure 12.4 illustrates this concept.

## Part IV: Analyzing Data in Microsoft Access

## FIGURE 12.3

In this query, you're using the aggregation results for each market as expressions in your calculation.

![](img/1e45673ab6eca9d20e67635ff5b9b318_425_0.png)

In this query, you're first calculating an adjusted forecast, and then you're using the results of that calculation in another calculation that returns the variance of actual versus adjusted forecast.

## FIGURE 12.4

This query uses the results of one calculation as an expression in another.

![](img/1e45673ab6eca9d20e67635ff5b9b318_425_1.png)

## Using a calculation as an argument in a function

Look at the query in Figure 12.5. The calculation in this query will return a number with a fractional part. That is, it will return a number that contains a decimal point followed by many trailing digits. You would like to return a round number, however, making the resulting data set easier to read.

## FIGURE 12.5

The results of this calculation will be difficult to read because they’ll all be fractional numbers that have many digits trailing a decimal point. Forcing the results into round numbers will make for easier reading.

![](img/1e45673ab6eca9d20e67635ff5b9b318_426_0.png)

To force the results of your calculation into an integer, you can use the Int function. The Int function is a mathematical function that will remove the fractional part of a number and return the resulting integer. This function takes one argument, a number. However, instead of hard-coding a number into this function, you can use your calculation as the argument. Figure 12.6 demonstrates this concept.

## FIGURE 12.6

You can use your calculation as the argument in the Int function, allowing you to remove the fractional part from the resulting data.

![](img/1e45673ab6eca9d20e67635ff5b9b318_426_1.png)

> **NOTE**
>
> You can use calculations that result in a numeric value in any function where a numeric value is accepted as an argument.

## Constructing calculations with the Expression Builder

If you aren’t yet comfortable manually creating complex expressions with functions and calculations, Access provides the Expression Builder. The Expression Builder guides you through constructing an expression with a few clicks of the mouse. Avid Excel users may relate the Expression Builder to the Insert Function Wizard found in Excel. The idea is that you build your expression simply by selecting the necessary functions and data fields.

To activate the Expression Builder, click inside the query grid cell that will contain your expression, right-click, and then select Build, as shown in Figure 12.7.

## FIGURE 12.7

Activate the Expression Builder by right-clicking inside the Field row of the query grid and selecting Build.

![](img/1e45673ab6eca9d20e67635ff5b9b318_427_0.png)

> **TIP**
>
> You can activate the Expression Builder by right-clicking anywhere you would write expressions, including control properties in forms, control properties in reports, and field properties in tables, as well as in the query design grid.

As you can see in Figure 12.8, the Expression Builder has four panes to work in. The upper pane is where you enter the expression. The lower panes show the different objects available to you. In the lower-left pane you can use the plus icons to expand the database objects that can be used to build out your expression.

## FIGURE 12.8

The Expression Builder will display any database object you can use in your expression.

![](img/1e45673ab6eca9d20e67635ff5b9b318_428_0.png)

Double-click any of the database objects to drill down to the next level of objects. By double-clicking the Functions object, for example, you'll be able to drill into the Built-In Functions folder where you'll see all the functions available to you in Access. Figure 12.9 shows the Expression Builder set to display all the available math functions.

## FIGURE 12.9

The Expression Builder displays all the functions available to you.

![](img/1e45673ab6eca9d20e67635ff5b9b318_428_1.png)

## Part IV: Analyzing Data in Microsoft Access

> **NOTE**
>
> If you're using a version of Access other than 2019, your Expression Builder will look slightly different from the one shown in Figure 12.9. However, the basic functionality remains the same.

The idea is that you double-click the function you need and Access will automatically enter the function in the upper pane of the Expression Builder. In the example shown in Figure 12.10, the selected function is the Round function. As you can see, the function is immediately placed in the upper pane of the Expression Builder, and Access shows you the arguments needed to make the function work. In this case, there are two arguments identified: a Number argument and a Precision argument.

## FIGURE 12.10

Access tells you which arguments are needed to make the function work.

![](img/1e45673ab6eca9d20e67635ff5b9b318_429_0.png)

If you don't know what an argument means, simply highlight the argument in the upper pane and then click the hyperlink at the bottom of the dialog box (see Figure 12.11). A Help window provides an explanation of the function.

## FIGURE 12.11

Help files are available to explain each function in detail.

![](img/1e45673ab6eca9d20e67635ff5b9b318_430_0.png)

As you can see in Figure 12.12, instead of using a hard-coded number in the Round function, an expression is used to return a dynamic value. This calculation will divide the sum of `[Dim_Transactions]![LineTotal]` by 13. Since the Precision argument is optional, that argument is left off.

## FIGURE 12.12

The function here will round the results of the calculation, `([Dim_Transactions]![Line Total]) / 13`.

![](img/1e45673ab6eca9d20e67635ff5b9b318_430_1.png)

When you are satisfied with your newly created expression, click OK to insert it into the query grid. Figure 12.13 shows that the new expression has been added as a field. Note that the new field has a default alias of Expr1; you can rename this to something more meaningful.

## FIGURE 12.13

Your newly created expression will give you the average revenue per period for all transactions.

![](img/1e45673ab6eca9d20e67635ff5b9b318_431_0.png)

## Common calculation errors

No matter which platform you’re using to analyze your data, there’s always the risk of errors when working with calculations. There is no magic function in Access that will help you prevent errors in your analysis. However, there are a few fundamental actions you can take to avoid some of the most common calculation errors.

## Understanding the order of operator precedence

You might remember from your algebra days that when working with a complex equation, executing multiple mathematical operations, the equation does not necessarily evaluate from left to right. Some operations have precedence over others and therefore must occur first. The Access environment has similar rules regarding the order of operator precedence. When you’re using expressions and calculations that involve several operations, each operation is evaluated and resolved in a predetermined order. It’s important to know the order of operator precedence in Access. An expression that is incorrectly built may cause errors in your analysis.

The order of operations for Access is as follows:

- 1. Evaluate items in parentheses.
- 2. Perform exponentiation (`^` calculates exponents).
- 3. Perform negation (`-` converts to negative).
- 4. Perform multiplication (`*` multiplies) and division (`/` divides) at equal precedence.

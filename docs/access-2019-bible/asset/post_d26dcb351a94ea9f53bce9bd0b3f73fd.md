
## NOTE

Keep in mind that the value returned when passing a date through a Format function is a string that cannot be used in subsequent calculations.

The query in Figure 12.29 shows how you would group all the order dates into quarters and then group the quarters to get a sum of revenue for each quarter.

## FIGURE 12.29

You can group dates into quarters by using the Format function.

![](img/1e45673ab6eca9d20e67635ff5b9b318_444_0.png)

If you want to get fancy, you can insert the Format function in a crosstab query, using Quarter as the column (see Figure 12.30).

As you can see in Figure 12.31, the resulting data set is a clean look at revenue by product by quarter.

## The DateSerial function

The DateSerial function allows you to construct a date value by combining given year, month, and day components. This function is perfect for converting disparate strings that, together, represent a date, into an actual date:

```
DateSerial(Year, Month, Day)
```

The DateSerial function has three arguments:

- Year (required): Any number or numeric expression from 100 to 9999
- Month (required): Any number or numeric expression
- Day (required): Any number or numeric expression

## Part IV: Analyzing Data in Microsoft Access

## FIGURE 12.30

You can also use the Format function in a crosstab query.

![](img/1e45673ab6eca9d20e67635ff5b9b318_445_0.png)

## FIGURE 12.31

You've successfully grouped your dates into quarters.

| Product_Name | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| Filter Sheets 13½" x 24" | $11,970.00 | $22,548.75 | $55,258.00 | $29,307.25 |
| Filter Sheets 14" x 22" | $28,284.60 | $57,696.10 | $190,679.15 | $125,965.20 |
| Filter Sheets 16½" x 23½" | $3,018.35 | $5,402.60 | $8,883.40 | $63,390.65 |
| Filter Sheets 18½" x 24½" | $49,286.10 | $101,954.70 | $106,431.90 | $111,335.50 |
| Food Warmer Pickup Stations 24" W |  | $7,967.60 | $15,529.50 | $9,389.10 |
| Food Warmer Pickup Stations 72" W | $11,804.00 | $16,532.80 |  |  |
| Fry Basket Black Handle |  | $3,366.00 |  |  |
| Fry Basket Yellow Handle |  |  | $7,469.40 | $6,965.40 |
| Fryer Brush |  |  | $7,160.00 | $11,592.00 |
| Funnel Cake Fryer | $3,497.00 | $6,325.15 | $49,318.10 | $143,146.99 |
| Garnish Center |  |  | $247,907.20 | $282,902.80 |
| ... | ... | ... | ... | ... |

For example, the following statement would return April 3, 2019:

```
DateSerial(2019, 4, 3)
```

So, how is this helpful? Well, now you can put a few twists on this by performing calculations on the expressions within the DateSerial function. Consider some of the possibilities:

- Get the first day of last month by subtracting 1 from the current month and using 1 as the Day argument:

```
DateSerial(Year(Date()), Month(Date()) - 1, 1)
```

## 1.2 常用逻辑用语

### 1.2.1 命题与量词

在数学中，我们把用语言、符号或式子表达的，可以判断真假的陈述句叫做命题(proposition)。其中判断为真的语句叫做真命题，判断为假的语句叫做假命题。

例如，下列语句中：

- (1) 12>3;
- (2) 3是15的约数;
- (3) 0.3是整数;
- (4) x>2;
- (5) 这是一棵大树;
- (6) x≥1.

其中(1)(2)是真的，(3)是假的，(4)(5)(6)无法判断真假，因此(1)(2)(3)是命题，(4)(5)(6)不是命题。

一般地，命题可以用语言表述，也可以用符号或式子表示。例如，上面的命题(1)(2)(3)可以分别表示为

12>3，3|15，0.3∈Z.

为了简洁，数学中通常把含有变量x的语句用p(x)，q(x)，r(x)等表示，并约定x的取值集合为U。例如

p(x): x+1≥0，x∈R.

表示“变量x的取值集合为R，x+1≥0”。

## CHAPTER 13

## Performing Conditional Analyses

## IN THIS CHAPTER

- Using parameter queries
- Using conditional functions
- Comparing the `IIf` and `Switch` functions

Until now your analyses have been straightforward. You build a query, you add some criteria, you add a calculation, you save the query, and then you run the query whenever you need to. What happens, however, if the criteria that governs your analysis changes frequently or if your analytical processes depend on certain conditions being met? In these situations, you would use a conditional analysis: an analysis whose outcome depends on a predefined set of conditions. Barring VBA and macros, there are several tools and functions that enable you to build conditional analyses; some of these are parameter queries, the IIf function, and the Switch function.

In this chapter, you learn how these tools and functions can help you save time, organize your analytical processes, and enhance your analyses.

> **ON THE WEB**
> The database for this walkthrough, `Chapter13.accdb`, can be downloaded from this book’s website.

## Using Parameter Queries

You’ll find that when building your analytical processes, anticipating every single combination of criteria that may be needed will often be difficult. This is where parameter queries can help.

A parameter query is an interactive query that prompts you for criteria before the query is run. A parameter query is useful when you need to ask a query different questions using different criteria each time it’s run. To get a firm understanding of how a parameter query can help you, build the query shown in Figure 13.1. With this query, you want to see all the purchase orders logged during the 201205 period.

## FIGURE 13.1

This query has a hard-coded criterion for system period.

![](img/1e45673ab6eca9d20e67635ff5b9b318_449_0.png)

Although this query will give you what you need, the problem is that the criterion for system period is hard-coded as 201205. That means if you want to analyze revenue for a different period, you essentially have to rebuild the query. Using a parameter query will allow you to create a conditional analysis—that is, an analysis based on variables you specify each time you run the query. To create a parameter query, simply replace the hard-coded criteria with text that you've enclosed in square brackets ([]), as shown in Figure 13.2.

## FIGURE 13.2

To create a parameter query, replace the hard-coded criteria with text enclosed in square brackets ([]).

![](img/1e45673ab6eca9d20e67635ff5b9b318_449_1.png)

Running a parameter query forces the Enter Parameter Value dialog box to open and ask for a variable. Note that the text you typed inside the brackets of your parameter appears in the dialog box. At this point, you would simply enter your parameter into a dialog box (see Figure 13.3).

## FIGURE 13.3

The Parameter Value dialog box lets you specify the criteria each time you run your query.

![](img/1e45673ab6eca9d20e67635ff5b9b318_450_0.png)

## How parameter queries work

When you run a parameter query, Access attempts to convert any text to a literal string by wrapping the text in quotes. However, if you place square brackets ([]) around the text, Access thinks that it's a variable and tries to bind some value to the variable using the following series of tests:

- 1. Access checks to see if the variable is a field name. If Access identifies the variable as a field name, that field is used in the expression.
- 2. If the variable is not a field name, Access checks to see if the variable is a calculated field. If Access determines the expression is indeed a calculated field, it simply carries out the mathematical operation.
- 3. If the variable is not a calculated field, Access checks to see if the variable is referencing an object such as a control on an open form or open report.
- 4. If all else fails, the only remaining option is to ask the user what the variable is, so Access displays the Enter Parameter Value dialog box, showing the text you entered in the Criteria row.

## Ground rules of parameter queries

As with other functionality in Access, parameter queries come with their own set of ground rules that you should follow in order to use them properly:

- You must place square brackets ([]) around your parameter. If you don't, Access will automatically convert your text into a literal string.
- You can't use the name of a field as a parameter. If you do, Access will simply replace your parameter with the current value of the field.
- You can't use a period (.), an exclamation point (!), square brackets ([]), or an ampersand (&) in your parameter's prompt text.
- You must limit the number of characters in your parameter's prompt text. Entering parameter prompt text that is too long may result in your prompt being cut off in the Enter Parameter Value dialog box. Moreover, you should make your prompts as clear and concise as possible.

> Tip
> If you really want to use a field name in your parameter's prompt, you can follow the field name with other characters. For example, instead of using [System_Period], you could use [System_Period: ?]. As you read this, keep in mind that there is nothing magic about the colon (:) or the question mark (?). Any set of characters will do. In fact, it may be more useful to provide your users with a sense of how the needed parameter should be formatted—for example: [System_Period: yyyymm].

## Working with parameter queries

The example shown in Figure 13.2 uses a parameter to define a single criterion. Although this is the most common way to use a parameter in a query, there are many ways to exploit this functionality. In fact, it's safe to say that the more innovative you get with your parameter queries, the more elegant and advanced your impromptu analysis will be. This section covers some of the different ways you can use parameters in your queries.

## Working with multiple parameter conditions

You aren't in any way limited in the number of parameters you can use in your query. Figure 13.4 demonstrates how you can utilize more than one parameter in a query. When you run this query, you'll be prompted for both a system period and a product ID, allowing you to dynamically filter on two data points without ever having to rewrite your query.

## Combining parameters with operators

You can combine parameter prompts with any operator you would normally use in a query. Using parameters in conjunction with standard operators allows you to dynamically expand or contract the filters in your analysis without rebuilding your query. To demonstrate how this works, build the query shown in Figure 13.5.

This query uses the BETWEEN...AND operator and the < (less than) operator to limit the results of the query based on the user-defined parameters. Since there are three parameter prompts built into this query, you'll be prompted for inputs three times: once for a starting period, once for an ending period, and once for a dollar amount. The number of records returned depends on the parameters you input. For instance, if you input 201201 as the starting period, 201203 as the ending period, and 5000 as the dollar amount, you'll get 1,700 records.

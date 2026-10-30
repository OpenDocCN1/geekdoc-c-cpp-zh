
# NOTE

Although the examples in this chapter show domain aggregate functions being used in query expressions, keep in mind that you can use these functions in macros, modules, or the calculated controls of forms and reports.

## The Anatomy of Domain Aggregate Functions

There are 12 different domain aggregate functions, but they all have the same anatomy:

```
FunctionName("[Field Name]", "[Dataset Name]", "[Criteria]*")
```

- **FunctionName**: This is the name of the domain aggregate function you're using.
- **Field Name (required)**: This expression identifies the field containing the data with which you're working.
- **Dataset Name (required)**: This expression identifies the table or query you're working with; also known as the domain.
- **Criteria (optional)**: This expression is used to restrict the range of data on which the domain aggregate function is performed. If no criteria is specified, the domain aggregate function is performed against the entire data set.

# NOTE

You can't use parameters as expressions in domain aggregate functions.

## Understanding the different domain aggregate functions

There are 12 different domain aggregate functions in Access, each performing a different operation. In this section, we take a moment to review the purpose and utility of each function.

### DSum

The DSum function returns the total sum value of a specified field in the domain. For example, DSum("[LineTotal]", "[Dim_Transactions]") would return the total sum of LineTotal in the Dim_Transactions table.

### DAvg

The DAvg function returns the average value of a specified field in the domain. For example, DAvg("[LineTotal]", "[Dim_Transactions]") would return the average LineTotal in the Dim_Transactions table.

### DCount

The DCount function returns the total number of records in the domain. DCount("*", "[Dim_Transactions]"), for example, would return the total number of records in the Dim_Transactions table.

### DLookup

The DLookup function returns the first value of a specified field that matches the criteria you define within the DLookup function. If you don’t supply a criteria or if the criteria you supplied doesn’t sufficiently identify a unique row, the DLookup function returns a random value in the domain. For example, DLookup("[Last_Name]", "[Employee_Master]", "[Employee_Number]=42620") would return the value in the Last_Name field of the record where the Employee_Number is 42620.

### DMin and DMax

The DMin and DMax functions return the minimum and maximum values in the domain, respectively. DMin("[LineTotal]", "[Dim_Transactions]") would return the lowest LineTotal in the Dim_Transactions table, whereas DMax("[LineTotal]", "[Dim_Transactions]") would return the highest LineTotal.

### DFirst and DLast

The DFirst and DLast functions return the first and last values in the domain, respectively. The following statement would return the first LineTotal in the Dim_Transactions statement:

```
DFirst("[LineTotal]", "[Dim_Transactions]")
```

The following statement would return the last LineTotal in the Dim_Transactions statement:

```
DLast("[LineTotal]", "[Dim_Transactions]")
```

Remember to use an ORDER BY clause to sort the field used in your DFirst or DLast function; otherwise, you will get a random value from that field.

### DStDev, DStDevP, DVar, and DVarP

You can use the DStDev and DStDevP functions to return the standard deviation across a population sample and a population, respectively. Similarly, the DVar and DVarP functions return the variance across a population sample and a population, respectively.

```
DStDev("[LineTotal]", "[Dim_Transactions]")
```

would return the standard deviation of all LineTotals in the Dim_Transactions table. DVar("[LineTotal]", "[Dim_Transactions]") would return the variance of all LineTotals in the Dim_Transactions table.

## Examining the syntax of domain aggregate functions

Domain aggregate functions are unique in that the syntax required to make them work actually varies depending on the scenario. This has led to some very frustrated users who have given up on domain aggregate functions altogether. This section describes some general guidelines that will help you in building your domain aggregate functions.

### Using no criteria

In this example, you’re summing the values in the LineTotal field from the Dim_Transactions table (domain). Your field names and data set names must always be wrapped in quotes.

```
DSum("[LineTotal]", "[Dim_Transactions]")
```

### Tip

Note the use of brackets. Although they are not always required, it's generally a good practice to use brackets when identifying a field, a table, or a query.

### Using text criteria

In this example, you're summing the values in the Revenue field from the PvTblFeed table (domain) where the value in the Branch_Number field is 301316. Note that the Branch_Number field is formatted as text. When specifying criteria that is textual or a string, your criteria must be wrapped in single quotes. In addition, your entire criteria expression must be wrapped in double quotes.

```
DSum("[Revenue]", "[PvTblFeed]", "[Branch_Number] = '301316'")
```

### Tip

You can use any valid WHERE clause in the criteria expression of your domain aggregate functions. This adds a level of functionality to domain aggregate functions, because they can support the use of multiple columns and logical operators such as AND, OR, NOT, and so on. An example would be:

```
DSum("[Field1]", "[Table]", "[Field2] = 'A' OR [Field2] = 'B' AND [Field3] = 2")
```

If you're referencing a control inside a form or report, the syntax will change a bit:

```
DSum("[Revenue]", "[PvTblFeed]", "[Branch_Number] = '" & [MyTextControl] & "'")
```

Notice that you're using single quotes to convert the control's value to a string. In other words, if the value of the form control is 301316, then

```
"[System_Period] = " & [MyTextControl] & """
```

is essentially translated to read

```
"[System_Period] = '301316'"
```

### Using number criteria

In this example, you're summing the values in the LineTotal field from the Dim_Transactions table (domain) where the value in the LineTotal field is greater than 500. Notice that you aren't using the single quotes since the LineTotal field is an actual number field.

```
DSum("[LineTotal]", "[Dim_Transactions]", "[LineTotal] > 500")
```

If you're referencing a control inside a form or report, the syntax will change a bit:

```
DSum("[LineTotal]", "[Dim_Transactions]", "[LineTotal] > " & [MyNumericControl])
```

## 1.1 计算机的诞生与发展

计算机（Computer）是一种能够按照程序运行，自动、高速处理海量数据的现代化智能电子设备。计算机的诞生与发展经历了多个重要阶段，从早期的机械计算工具到现代的电子计算机，每一次变革都极大地推动了人类社会的进步。

### 1.1.1 早期计算工具

在电子计算机出现之前，人类已经发明了多种计算工具。中国古代的算筹和算盘是最早的计算工具之一，它们通过手动操作来进行加减乘除等基本运算。17世纪，法国数学家帕斯卡发明了第一台机械计算器——帕斯卡加法器，能够进行加减法运算。随后，德国数学家莱布尼茨对其进行了改进，设计出了能够进行四则运算的步进计算器。

### 1.1.2 电子计算机的诞生

20世纪40年代，电子计算机的诞生标志着计算技术进入了一个全新的时代。1946年，美国宾夕法尼亚大学研制成功了世界上第一台通用电子计算机ENIAC（埃尼阿克），它使用了18000多个电子管，占地170平方米，重达30吨，每秒可进行5000次加法运算。虽然ENIAC体积庞大、功耗极高，但它奠定了电子计算机发展的基础。

### 1.1.3 计算机的发展阶段

自电子计算机诞生以来，根据其采用的电子器件不同，计算机的发展大致经历了四个阶段：

- **第一代（1946—1958年）：电子管计算机**。采用电子管作为基本逻辑元件，主存储器采用磁鼓，外存储器采用磁带。体积大、功耗高、速度慢，主要用于科学计算。
- **第二代（1958—1964年）：晶体管计算机**。采用晶体管代替电子管，体积缩小、功耗降低、速度提高，主存储器采用磁芯，软件开始使用高级语言。
- **第三代（1964—1971年）：集成电路计算机**。采用中小规模集成电路，使计算机体积更小、功耗更低、可靠性更高，操作系统和多种高级语言得到广泛应用。
- **第四代（1971年至今）：大规模集成电路计算机**。采用大规模和超大规模集成电路，微处理器问世，个人计算机（PC）迅速普及，计算机进入了网络化和智能化时代。

## Part IV: Analyzing Data in Microsoft Access

To get the percent of the total dollar value that each product makes up, you naturally would have to know the total dollar value of the entire data set. This is where a DSum function can come in handy. The following DSum function will return the total value of the data set:

```
DSum("[LineTotal]", "[Dim_Transactions]")
```

Now you can use this function as an expression in the calculation that will return the percent of total for each product group. Figure 15.16 demonstrates how.

### FIGURE 15.16

Use a DSum function as an expression in a calculation to get percent of total.

![](img/1e45673ab6eca9d20e67635ff5b9b318_507_0.png)

The result, shown in Figure 15.17, proves that this is a quick and easy way to get both total by group and percent of total with one query.

### FIGURE 15.17

You retrieved both total by group and percent of total with one query.

![](img/1e45673ab6eca9d20e67635ff5b9b318_507_1.png)

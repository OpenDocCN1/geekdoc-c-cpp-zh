# 12. (Program) a. A bookstore summarizes its monthly transactions by keeping the following information for each book in stock:

+   - Book identification number
+   - Inventory balance at the beginning of the month
+   - Number of copies received during the month
+   - Number of copies sold during the month

Write a C++ program that accepts this data for each book and then displays the book identification number and an updated book inventory balance, using this relationship:

New balance = Inventory balance at the beginning of the month
+ Number of copies received during the month
- Number of copies sold during the month

Your program should use a while statement with a fixed-count condition so that information on only three books is requested.

b. Compile and run the program written in Exercise 12a. Review the display your program produces and verify that the output is correct.

# 13. (Modify) Modify the program you wrote for Exercise 12 to keep requesting and displaying results until a sentinel value of 999 is entered. Compile and run your program. Review the display your program produces and verify that the output is correct.

# 5.3 The for Statement

A for statement performs the same functions as the while statement but uses a different form. In many situations, especially those using a fixed-count condition, the for statement's format is easier to use than the while statement equivalent. This is the general form of the for statement:

```
for (initializing list; expression; altering list)
    statement;
```

Although the for statement looks a little complicated, it's really quite simple if you consider each part separately. Inside the parentheses of the for statement are three items, separated by semicolons. Each item is optional and can be described separately, but the semicolons must always be present, even if you don't use the items. As you'll see, the items in parentheses correspond to the initialization, expression evaluation, and expression altering values you've already used with the while statement.

Typically, variables need to be initialized or other evaluations need to be made before entering a repetition loop, so the for statement allows grouping all initializing statements as the first set of items inside for's parentheses. The items in this initializing list are executed only once, before the expression is evaluated for the first time.

The middle item in parentheses, expression, is any valid C++ expression, and there's no difference in the way for and while statements use this expression. In both statements, as long as the expression has a non-zero (true) value, the statement following the parentheses is
reaches the else keyword, it will not associate it with the previous if statement; instead, it will report a syntax error. Therefore, it is good practice to always define the statements for each branch of an if statement within a block, even if a block consists of only a single statement. It might save you some grief later if you want to add more code.

A block also starts a scope. You can define variables inside a block, they will disappear at the end of the block. The following code fragment illustrates this point:

Click here to view code image

```
if (...)
{
    int myVar = 0;
    // myVar can be used here
} // myVar disappears here
else
{
    // myVar cannot be used here
}
myVar cannot be used here
```

# Cascading if statements

You can nest if statements inside other if statements. In this way, you can chain a sequence of Boolean expressions, which are tested one after the other until one of them evaluates to true.

In the following example, the value of day is 0, the first evaluates to true, and dayName is assigned the string "Sunday". If the value of day is not 0, the first test fails, and control passes to the else clause, which runs the second if statement and compares the value of day with 1. The second if statement executes only if the first is false. Similarly, the third if statement executes only if the first and second tests are false, and so on.

```
if (day == 0)
{
    dayName = "Sunday";
}
 if (day == 1)
```
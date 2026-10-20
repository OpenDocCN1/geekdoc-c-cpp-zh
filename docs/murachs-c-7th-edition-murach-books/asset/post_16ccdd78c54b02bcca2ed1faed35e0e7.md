
## How to code conditional statements and expressions

Now that you know how to code Boolean expressions, you’re ready to learn how to code conditional statements and expressions. That includes the if-else and switch statements, the switch expression, and expressions that use the conditional operator.

### How to code if-else statements

Figure 5-3 shows how to use the *if-else statement* (or just *if statement*) to control the logic of your programs. This type of statement is the primary logical statement of all programming languages. It is the C# implementation of a control structure known as the *selection structure* because it lets you select different actions based on the results of Boolean expressions.

In the syntax summary in this figure, the brackets [ ] indicate that a clause is optional, and the ellipsis (...) indicates that the preceding element can be repeated as many times as needed. In other words, this syntax shows that you can code an *if* clause with or without *else if* clauses or an *else* clause. It also shows that you can code as many else if clauses as you need.

When an if statement is executed, C# begins by evaluating the Boolean expression in the if clause. If it’s true, the statements within this clause are executed and the rest of the clauses in the if-else statement are skipped. If it’s false, C# evaluates the first else if clause (if there is one). If its Boolean expression is true, the statements within this else if clause are executed and the rest of the if-else statement is skipped. Otherwise, C# evaluates the next else if clause. This continues with any remaining else if clauses. Finally, if none of the clauses contains a Boolean expression that evaluates to true, C# executes the statements in the else clause. If the statement doesn’t include an else clause, C# doesn’t execute any statements.

When coding if-else statements, it’s often a good coding practice to code a set of braces for each clause. However, if a clause only contains a single statement, you can omit the braces. Although omitting the braces saves you some typing and takes up less vertical space, coding the braces makes it easier to identify the statements for each clause, and it makes it easier for you to add more statements later.

If you’re working on an existing project that doesn’t include the braces, you can add them using refactoring. To do that, place the cursor in an if, else if, or else clause, press Ctrl + period (.), and select Add Braces from the Quick Actions menu that’s displayed. Then, click the Document, Project, or Solution link in the popup window to identify where you want the changes made.

In C#, whenever you use braces, you define a block of code. If you declare a variable within a block, that variable is available only to the other statements in the block. This can be referred to as *block scope*. As a result, if you need to access a variable outside of an if statement, you should declare it before the if statement.

When coding if statements, it’s a common practice to code one if statement within another if statement. This is known as *nested if statements*. When you code nested if statements, it’s a good practice to indent the nested statements and their clauses. This clearly identifies where the nested statement begins and ends. In the last example in this figure, you can see that C# will execute the nested if statement only if the customer type is R. Otherwise, it executes the statement in the outer else clause.

### How to code switch statements

Figure 5-4 shows how to use the *switch statement*. This is the C# implementation of a control structure known as the *case structure*, which lets you code different actions for different cases. The switch statement can sometimes be used in place of an if statement with else if clauses.

To code a switch statement, you start by coding the switch keyword followed by a *match expression*. This expression must evaluate to one of the data types listed in this figure. After the match expression, you can code one or more *case labels* that represent the possible values of the match expression. Then, when the match expression matches the value specified by a case label, the statements that follow the label are executed. A switch statement can also contain a *default label* that identifies the statements that are executed if none of the values specified by the case labels match the match expression. All of these case labels are coded within the switch statement braces.

When you code a case label or a default label, you must be sure to code a colon after it. Then, if the label contains one or more statements, you must code a *break statement* to exit the switch statement. Later in this chapter, you’ll see that you can also use break statements to exit loops.

A break statement is required for each label within a switch statement because C# doesn’t allow execution to *fall through* to the next label. This is known as the *no fall through rule*. The only exception to this rule is a case label that doesn’t contain any statements. In that case, the statements within the following label are executed.

The first example in this figure shows how to code a switch statement that sets the discount percent based on the values in a string variable named customerType. If the customer type is R, the discount percent is set to .1. If the customer type is C, the discount percent is set to .2. Otherwise, the discount percent is set to the default value of 0.

Please note in this example that even though the default label is the last label, it must still end with a break statement. You should also realize that you can code the case and default labels in any sequence. However, it’s a common practice to code the default label last.

The second example is similar but it doesn’t include a default label. Because of that, no code will be executed if none of the values in the case labels match the match expression. The other difference is that the first case label doesn’t include any statements. Because of that, if the customer type is R, execution falls through to the next case label. That means that the discount percent will be set to .2 if the customer type is either R or C.

### The syntax of the switch statement

```text
switch (matchExpression)
{
    case constantExpression:
        statements
        break;
    [case constantExpression:
        statements
        break;] ...
    [default:
        statements
        break;]
}
```

### A switch statement with a default label

```text
switch (customerType)
{
    case "R":
        discountPercent = .1m;
        break;
    case "C":
        discountPercent = .2m;
        break;
    default:
        discountPercent = .0m;
        break;
}
```

### A switch statement that falls through the first case label

```text
switch (customerType)
{
    case "R":
    case "C":
        discountPercent = .2m;
        break;
    case "U":
        discountPercent = .4m;
        break;
}
```

### Description

- A *switch statement* begins by evaluating its *match expression*. This expression must evaluate to a string, char, bool, enum, or any integer type.
- After evaluating the match expression, the switch statement transfers control to the appropriate *case label*. If control isn’t transferred to one of the case labels, the optional *default label* is executed.
- The *break statement* exits the switch statement. If a label contains one or more statements, the label must end with a break statement.
- If a label doesn’t contain any statements, code execution will *fall through* to the next label. That means that the statements contained by the next label will be executed.

![](img/844f608d10a44654833ea5efc8a2e7a7_164_0.png)

When you use a switch statement, you can code if statements within the cases of the statement. You can also code switch statements within the cases of another switch statement. That can make switch statements more useful. Generally, though, programmers prefer to use if-else statements instead of switch statements because if-else statements aren’t as limited.

### How to code switch expressions

With C# 8.0 and later, you can use *switch expressions* in addition to switch statements. Switch expressions work like switch statements, but their syntax is more concise. Figure 5-5 shows how to code switch expressions.

The syntax at the top of this figure shows that, unlike a switch statement, you code the match expression before the switch keyword for a switch expression. This was done intentionally to make it easy to distinguish between switch statements and switch expressions.

Within the braces that follow the switch keyword, you code one or more constant expressions that represent the possible values of the match expression. Although you don’t code these expressions on case labels, they are still often referred to as cases since a switch expression provides another way of implementing the case structure. After each constant expression, you code a *lambda operator* (=>, read as “goes to”), followed by the expression to be returned. This is different from a switch statement, where each case label can contain multiple executable statements.

A switch expression can also include a default expression that’s returned if none of the constant expressions match the match expression. To identify this expression, you use a *discard* (_). This is equivalent to the default label that you can use with switch statements. Discards were introduced with C# 7.0 and can also be used with out parameters and tuples, as you’ll see in chapter 6.

Notice that the cases within a switch expression are separated by commas. In addition, a switch expression must end with a semicolon (;). That’s because a switch expression is treated as a single statement.

The first example in this figure illustrates how a simple switch expression works. Here, the switch expression is used to assign a value to the discountPercent variable based on the value of the customerType variable. If the customer type is R, for example, the discount percent is set to .1. If the customer type is C, the discount percent is set to .2. And if the customer type is something other than R or C, the discount percent is set to 0. This accomplishes the same thing as the first switch statement in figure 5-4. If you compare this switch expression and switch statement, though, you’ll see that the switch expression requires less code.

The second example is similar to the first, except that it returns the same value for customer types R and C. To do that, it must repeat the value for each type. That’s because the cases of a switch expression can’t fall through to the next case like they can in a switch statement. Even so, this code is still concise and clear, as you’ll see if you compare this switch expression with the second switch statement in figure 5-4.

The third example shows that the expression for each case can be more than just a constant value. Here, the switch expression returns the discount amount for

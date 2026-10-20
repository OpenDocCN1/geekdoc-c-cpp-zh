each customer type. To do that, the first three expressions multiply the subtotal by a discount percent. This should help you begin to see the types of expressions that you can code for the cases of a switch expression.

With C# 9.0 and later, you can use relational operators in a switch statement or expression as shown by the fourth example. Here, the constant expressions use relational operators to calculate a discount amount based on the range of the subtotal. Note that the first constant expression uses the and keyword to connect two relational operators. This capability was introduced with C# 9.0.

Now that you’ve seen how switch expressions work, you may be wondering when you would use them. In most cases, you’ll use them when you simply need to assign a value to a variable as shown in the examples.

# How to use the conditional operator

So far in this book, you’ve seen unary operators that take a single operand and binary operators that take two operands. Now, figure 5-6 shows how to use the conditional operator. This operator is known as a ternary operator because it takes three operands. The first operand is a Boolean expression, the second operand is an expression that’s evaluated and returned if the Boolean expression is true, and the third operand is an expression that’s evaluated and returned if the Boolean expression is false.

The conditional operator requires two symbols to separate its three operands. This is illustrated by the syntax for a conditional expression, which is an expression that uses the conditional operator. As you can see, the question mark (?) is used to separate the Boolean expression and the true expression, and the colon (:) is used to separate the true and the false expressions.

The first example shows a conditional expression. Here the Boolean expression checks if the variable named subtotal is greater than or equal to 100. If it is, it returns .1. Otherwise, it returns .05.

The second example shows how you would use a conditional expression in an assignment statement. Here, the statement begins by declaring a decimal variable named discountPercent. Then, it assigns the result of the conditional expression in the first example to that variable. As a result, if the subtotal is greater than or equal to 100, the discountPercent variable is .1. Otherwise, it’s .05.

The third example works the same as the second example. However, it uses parentheses to clearly identify the Boolean expression. These parentheses are optional, but some programmers prefer using them because they make it easier to read the statement.

The fourth example shows the third example after it has been rewritten to use an if statement instead of the conditional operator. This shows that a statement that uses the conditional operator can always be rewritten to use an if statement. Some programmers prefer this approach, since they consider if statements easier to read. Other programmers like to use the conditional operator because it takes fewer lines of code. As a result, even if you don’t use the conditional operator in your code, you still need to understand how it works so you can understand code that has been written by other programmers.
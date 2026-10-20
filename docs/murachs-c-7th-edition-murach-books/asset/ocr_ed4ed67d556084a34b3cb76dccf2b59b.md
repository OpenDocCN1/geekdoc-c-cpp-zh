# How to code expression-bodied methods

In the last chapter, you saw that you can use the lambda operator (=>) to return an expression for the cases in a switch expression. Now, figure 6-4 shows how to use the lambda operator to code *expression-bodied methods*, which became available with C# 6.0.

An expression-bodied method can return the value of an expression or execute a single statement. For instance, the first example in this figure shows a method named DisplayErrorMessage() that contains a single statement that displays a message box with the message and caption that are passed to it.

The statement that follows shows how to code this method using an expression-bodied method. To do that, you code the method signature just like you do for any other method, followed by the lambda operator and the statement to be executed. This provides a minor simplification by eliminating the need for the braces.

The second example shows a method that returns a discount percent based on the customer type that’s passed to it. This method uses a switch expression like the ones you learned about in chapter 5 to get the discount percent. This switch expression is coded on a return statement so the result of the expression is returned to the calling code.

To code this method as an expression-bodied method, you add the lambda operator, omit the braces for the method, and omit the return statement as shown here. Once again, this provides a minor simplification to the code. As you continue with this book, though, you’ll see that the lambda operator can be used in a number of different situations. So it’s best to become familiar with it right away by using it whenever that makes sense.
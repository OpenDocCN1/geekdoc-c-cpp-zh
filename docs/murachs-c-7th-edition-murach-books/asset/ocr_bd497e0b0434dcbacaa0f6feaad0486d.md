# How to call methods

Figure 6-2 shows how to call a method that’s coded within a form class. By now, you should be familiar with the basic syntax for calling a method, so most of this figure should be review. To start, you can type the optional *this* keyword to specify that the method that’s being called is in the current class, followed by the dot operator and the method name. Otherwise, you just code the method name and the current class is assumed.

If the method requires *arguments*, you code the *argument list* within parentheses right after the method name. Otherwise, you code an empty set of parentheses. Before I go on, you should realize that the terms *parameter* and *argument* are often used interchangeably. In this book, however, we’ll use the term *parameter* to refer to the variables of a method declaration, and we’ll use the term *argument* to refer to the values that are passed to a method.

When you call a method, you typically code the arguments in the same sequence that’s used by the parameter list in the method. This is called *passing arguments by position*. You can also pass arguments by name, as you’ll see shortly.

When you pass arguments, the data types of those arguments must be compatible with the data types of the corresponding parameters in the method. In fact, it’s a good coding practice to pass arguments that have the *same* data types as the parameters in the method. Note, however, that the argument names don’t have to be the same as the parameter names. But this is a common practice that makes code easier to read and write.

The three examples in this figure show how you would call the three methods you saw in figure 6-1. The first example calls the DisableButtons() method, which has no parameters. Because of that, the statement call doesn’t include any arguments. In addition, the method doesn’t return any data, so the statement simply calls the method.

The second example calls the GetDiscountPercent() method. Since this method is defined with one parameter, the statement that calls it passes one argument. In this case, the argument is a variable named subtotal. However, you could also code the argument as a literal value, such as 49.50m. In addition, because this method returns a value, the method call is coded as part of an assignment statement. When this statement is executed, the return value from the method, which is declared with the decimal type, is assigned to the discountPercent variable, which is also declared as a decimal.

The third example shows how to call a method that requires three arguments. In this case, all three arguments have the same data types as the corresponding parameters in the method. In addition, the arguments are listed in the same order as the corresponding parameters.

When you call a method that returns a value, you can assign that value to a variable as shown in the second and third examples in this figure. However, you can also code a method call within an expression. For example, you could use the GetDiscountPercent() method in an expression like this:

```
total = subtotal * (1 - this.GetDiscountPercent(subtotal));
```

In this case, the decimal value that’s returned by the method will be used to perform a calculation.
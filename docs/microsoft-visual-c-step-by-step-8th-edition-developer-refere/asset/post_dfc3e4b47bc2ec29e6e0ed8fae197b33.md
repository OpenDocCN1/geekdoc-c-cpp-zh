
private void showIntValue()
{
    int intVar;
    intVar = 42;
    value.Text = "to do";
}

The first statement creates a variable called intVar that can hold an int value. The second statement assigns the value 42 to this variable.

8. In the original statement in this method, change the string “to do” to intVar.ToString();

The method should now look exactly like this:

Click here to view code image

```
private void showIntValue()
{
    int intVar;
    intVar = 42;
    value.Text = intVar.ToString();
}
```

9. On the Debug menu, click Start Debugging.

The form appears again.

10. In the Choose A Data Type list, select the int type. Confirm that the value 42 is displayed in the Sample Value text box.

11. Return to Visual Studio and then, on the Debug menu, click Stop Debugging.

12. In the Code and Text Editor window, find the showDoubleValue method.

13. Edit the showDoubleValue method exactly as shown in bold type in the following code:

Click here to view code image

```
private void showDoubleValue()
{
    double doubleVar;
    doubleVar = 0.42;
    value.Text = doubleVar.ToString();
}
```

This code is similar to the showIntValue method, except that it creates a variable called doubleVar that holds double values and is assigned the value 0.42.

14. In the Code and Text Editor window, locate the showBoolValue method.

15. Edit the showBoolValue method exactly as follows:

Click here to view code image

```
private void showBoolValue()
{
bool boolVar;
boolVar = false;
value.Text = boolVar.ToString();
}
```

Again, this code is similar to the previous examples, except that *boolVar* can only hold a Boolean value, *true* or *false*. In this case, the value assigned is *false*.

+   16. On the Debug menu, click Start Debugging.

+   17. In the Choose A Data Type list, select the *float*, *double*, and *bool* types. In each case, verify that the correct value is displayed in the Sample Value text box.

+   18. Return to Visual Studio and then, on the Debug menu, click Stop Debugging.

## Using arithmetic operators

C# supports the regular arithmetic operations you learned in your childhood: the plus sign (+) for addition, the minus sign (−) for subtraction, the asterisk (*) for multiplication, and the forward slash (/) for division. The symbols +, −, *, and / are called *operators* because they “operate” on values to create new values. In the following example, the variable *moneyPaidToConsultant* ends up holding the product of 750 (the daily rate) and 20 (the number of days the consultant was employed):

Click here to view code image

```
long moneyPaidToConsultant;
moneyPaidToConsultant = 750 * 20;
```

### Note

The values on which an operator performs its function are called *operands*. In the expression 750 * 20, the * is the operator, and 750 and 20 are the operands.

## Operators and types

Not all operators are applicable to all data types. The operators that you can use on a value depend on the value’s type. For example, you can use all the arithmetic operators on values of type *char*, *int*, *long*, *float*, *double*, or *decimal*. However, with the exception of the plus operator (+), you can’t use the arithmetic operators on values of type *string*, and you cannot use any of them with values of type *bool*. So, the following statement is not allowed because the *string* type does not support the minus operator (subtracting one string from another is meaningless):

Click here to view code image

```
// compile-time error
Console.WriteLine("Gillingham" - "Forest Green Rovers");
```

However, you can use the + operator to concatenate string values. You need to be careful because this can have unexpected results. For example, the following statement writes “431” (not “44”) to the console:

Click here to view code image

```
Console.WriteLine("43" + "1");
```

### Tip

The .NET Framework provides a method called Int32.Parse that you can use to convert a string value to an integer if you need to perform arithmetic computations on values held as strings.

## String interpolation

A new feature in the latest version of C# is string interpolation, which renders many uses of the + operator obsolete for concatenating strings.

A common use of string concatenation is to generate string values that include variable values. You saw an example of this in the exercises in Chapter 1 that created a graphical application. In the okClick method you added the following line of code:

```
MessageDialog msg = new MessageDialog("Hello " + userName.Text);
```

String interpolation lets you use the following syntax instead:

```
MessageDialog msg = new MessageDialog($"Hello {userName.Text}");
```

The $ symbol at the start of the string indicates that it is an interpolated string and that any expressions between the { and } characters should be evaluated and the result substituted in their place. Without the leading $ symbol, the string {username.Text} would be treated literally.

String interpolation is more efficient than using the + operator. (String concatenation using the + operator can be memory hungry by virtue of the way in which strings are handled by the .NET Framework.) String interpolation is also arguably more readable and less error prone.

You should also be aware that the type of the result of an arithmetic operation

depends on the type of the operands used. For example, the value of the expression 5.0/2.0 is 2.5; the type of both operands is *double*, so the type of the result is also *double*. (In C#, literal numbers with decimal points are always *double*, not *float*, to maintain as much accuracy as possible.) However, the value of the expression 5/2 is 2. In this case, the type of both operands is *int*, so the type of the result is also *int*. C# always rounds toward zero in circumstances like this. The situation gets a little more complicated if you mix the types of the operands. For example, the expression 5/2.0 consists of an *int* and a *double*. The C# compiler detects the mismatch and generates code that converts the *int* into a *double* before performing the operation. The result of the operation is therefore a *double* (2.5). However, although this works, it is considered poor practice to mix types in this way.

C# also supports one less-familiar arithmetic operator: the *remainder*, or *modulus*, operator, which is represented by the percent sign (%). The result of *x* % *y* is the remainder after dividing the value *x* by the value *y*. So, for example, 9 % 2 is 1 because 9 divided by 2 is 4, remainder 1.

### Note

If you are familiar with C or C++, you know that you can’t use the remainder operator on *float* or *double* values in these languages. However, C# relaxes this rule. The remainder operator is valid with all numeric types, and the result is not necessarily an integer. For example, the result of the expression 7.0 % 2.4 is 2.2.

## Numeric types and infinite values

There are one or two other features of numbers in C# about which you should be aware. For example, the result of dividing any number by zero is infinity, which is outside the range of the int, long, and decimal types; consequently, evaluating an expression such as 5/0 results in an error. However, the double and float types actually have a special value that can represent infinity, and the value of the expression 5.0/0.0 is Infinity. The one exception to this rule is the value of the expression 0.0/0.0. Usually, if you divide zero by anything, the result is zero, but if you divide anything by zero the result is infinity. The expression 0.0/0.0 results in a paradox—the value must be zero and infinity at the same time. C# has another special value for this situation called NaN, which stands for “not a number.” So if you evaluate 0.0/0.0, the result is NaN.

NaN and Infinity propagate through expressions. If you evaluate 10 + NaN, the result is NaN, and if you evaluate 10 + Infinity, the result is Infinity. The value of the expression Infinity * 0 is NaN.

## Examining arithmetic operators

The following exercise demonstrates how to use the arithmetic operators on int values.

## Run the MathsOperators project

+   1. Start Visual Studio 2015 if it is not already running.
+   2. Open the MathsOperators project, located in the \Microsoft Press\VCSBS\Chapter 2\MathsOperators folder in your Documents folder.
+   3. On the Debug menu, click Start Debugging.

The following form appears:

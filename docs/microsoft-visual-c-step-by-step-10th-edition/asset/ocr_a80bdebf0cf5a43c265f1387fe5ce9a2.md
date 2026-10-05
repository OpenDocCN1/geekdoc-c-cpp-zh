Only integer arithmetic directly inside the checked block is subject to overflow checking. For example, if one of the checked statements is a method call, checking does not apply to code that runs in the called method.

You can also use the unchecked keyword to create an unchecked block statement. All integer arithmetic in an unchecked block is not checked and never throws OverflowException. For example:

Click here to view code image

```
int number = int.MaxValue;
{
  int wontThrow = number++;
  Console.WriteLine("This will be reached");
}
```

# Writing checked expressions

You can also use the checked and unchecked keywords to control overflow checking on integer expressions by preceding just the individual parenthesized expression with the checked or unchecked keyword, as shown in these examples:

Click here to view code image

```
int wontThrow = unchecked(int.MaxValue + 1);
int willThrow = checked(int.MaxValue + 1);
```

The compound operators as += and --= and the increment (++) and decrement (--) operators are arithmetic operators and can be controlled using the checked and unchecked keywords. Remember, x += y is the same as x = x + y.

> Important
You cannot use the checked and unchecked keywords to control floating-point(noninteger) arithmetic. The checked and unchecked keywords apply only to integer arithmetic using data types such as int and long. Floating-point arithmetic never throws OverflowException exceptions—not even when you divide by 0.0. (Remember from Chapter 2 that .NET has a special floating-point representation for infinity.)
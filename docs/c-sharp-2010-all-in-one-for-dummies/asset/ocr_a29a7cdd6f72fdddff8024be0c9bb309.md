```
Interest paid = 0
Total = 1234
Press Enter to terminate . . .
```

![](bbox=[0.08, 0.25, 0.2, 0.38])

Indent the lines within an if clause to enhance readability. This type of indentation is ignored by C# but is helpful to us humans. Most programming editors support autoindenting, whereby the editor automatically indents as soon as you enter the if command. To set autoindenting in Visual Studio, choose Tools→Options. Then expand the Text Editor node. From there, expand C#. Finally, click Tabs. On this page, enable Smart Indenting and set the number of spaces per indent to your preference. (I use two spaces per indent in this book.) Set the tab size to the same value.

# Examining the else statement

Sometimes, your code must check for mutually exclusive conditions. For example, the following code segment stores the maximum of two numbers, a and b, in the variable max:

```
// Store the maximum of a and b into the variable max.
int max;
// If a is greater than b . . .
if (a > b)
{
  // . . . save a as the maximum.
  max = a;
}
// If a is less than or equal to b . . .
if (a <= b)
{
  // . . . save b as the maximum.
  max = b;
}
```

The second if statement causes needless processing because the two conditions are mutually exclusive. If a is greater than b, it can't possibly be less than or equal to b. C# defines an else clause for just this case. The else keyword defines a block of code that's executed if the if block is not.

The code segment to calculate the maximum now appears this way:

```
// Store the maximum of a and b into the variable max.
int max;
// If a is greater than b . . .
if (a > b)
{
  // . . . save a as the maximum; otherwise . . .
  max = a;
}
else
{
  // . . . save b as the maximum.
  max = b;
}
```
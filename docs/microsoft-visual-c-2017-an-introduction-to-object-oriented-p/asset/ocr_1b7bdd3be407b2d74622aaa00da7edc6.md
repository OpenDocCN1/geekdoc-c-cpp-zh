# You Do It

Using if-else Statements

In the next steps, you write a program that requires using multiple, nested if-else statements to accomplish its goal—determining whether any of the three integers entered by a user are equal.

+   1. Open a new file or project named CompareThreeNumbers, and write the first lines necessary for the class:

```
using System;
using static System.Console;
class CompareThreeNumbers
{
```

+   2. Begin a Main() method by declaring a string for input and three integers that will hold the input values.

```
static void Main()\{
    string numberString;
    int num1, num2, num3;
```

+   3. Add the statements that retrieve the three integers from the user and assign them to the appropriate variables.

```
Write("Enter an integer ");
numberString = ReadLine();
num1 = Convert.ToInt32(numberString);
Write("Enter an integer ");
numberString = ReadLine();
num2 = Convert.ToInt32(numberString);
Write("Enter an integer ");
numberString = ReadLine();
num3 = Convert.ToInt32(numberString);
```

In the chapter "Introduction to Methods," you will learn to write methods, which will allow you to avoid repetitive code like that shown here.

(continues)
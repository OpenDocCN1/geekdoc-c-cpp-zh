If the value of weight is less than 50, then the following statement is executed, which in turn is another if statement. This if statement tests height and if the height is greater than 170, then the count is incremented by 1. Program 6.1 illustrates the implementation of the above statement.

# Program 6.1 COUNTING WITH IF STATEMENT

```
using System;
class IfTest
{
    public static void Main()
    {
        int i, count, count1, count2;
        float[] weight = { 45.0F,55.0F,47.0F,51.0F,54.0F };
        float[] height = { 176.5F,174.2F,168.0F,170.7F,169.0F };

        count = 0;
        count1 = 0;
        count2 = 0;

        for (i = 0; i <= 4; i++)
        {
            if(weight[i] < 50.0 && height[i] > 170.0)
            {
                count1 = count1 + 1; // Executed when condition is true
            }
            count = count + 1;   // Always executed
        }
        count2 = count - count1;
        Console.WriteLine("Number of persons with ...");
        Console.WriteLine("Weight<50 and height>170 = "+count1);
        Console.WriteLine("Others = " + count2);
    }
}
```

The output of Program 6.1 will be:
    Number of persons with ...
    Weight<50 and height>170 = 1
    Others = 4

C and C++ programmers must note that in C# the expression in an if statement must resolve to a bool value. We cannot use integer values, like if(x).... Arrays are discussed in Chapter 9.

# 6.4 THE IF... ELSE STATEMENT

The if...else statement is an extension of the simple if statement. The general form is

```
if(boolean_expression)
{
    True-block statement(s)
}
else
{
```
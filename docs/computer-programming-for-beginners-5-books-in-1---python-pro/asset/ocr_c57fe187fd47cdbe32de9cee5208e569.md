![](bbox=[0.034, 0.026, 0.88, 0.236])

# Multicast Delegate

It is possible for a delegate to point to multiple functions. Any delegate that points to many functions is referred to as a *multicast delegate*. Use the + operator to add a function to a delegate object and the − operator to remove an existing function from a delegate object.

Consider the example given below:

```
using System;
public class MyProgram
{
    public delegate void Display(int value);

    public static void Main()
    {
        Display displayDel = DisplayNumber;
        displayDel += DisplayHexadecimal;
        displayDel += DisplayMoney;

        displayDel(1000);
        displayDel -= DisplayHexadecimal;
        displayDel(2000);
    }
    public static void DisplayNumber(int x)
    {
```
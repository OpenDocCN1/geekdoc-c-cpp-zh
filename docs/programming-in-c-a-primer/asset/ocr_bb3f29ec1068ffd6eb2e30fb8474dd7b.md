```
if(sex is female)
{
    if (balance > 5000)
        bonus = 0.05 * balance;
}
else
    bonus = 0.02 * balance;
    balance = balance + bonus;
```

In this case, else is associated with the outer if and therefore bonus is calculated for the male account holders. However, bonus for the female account holders, whose balance is equal to or less than 5000 is not calculated because of the missing else option for the inner if.

Program 6.4 employs nested if....else statements to determine the largest of three given numbers.

# Program 6.4    NESTING IF....ELSE STATEMENTS

```
using System;
class IfElseNesting
{
    public static void Main()
    {
        int a = 325, b = 712, c = 478;

        Console.Write("Largest value is : ");
        if (a > b)
        {
            if (a > c)
            {
                Console.WriteLine(a);
            }
            else
            {
                Console.WriteLine(c);
            }
        }
        else
        {
            if (c > b)
            {
                Console.WriteLine(c);
            }
            else
            {
                Console.WriteLine(b);
            }
        }
    }
}
```
>>= is a composite operator. It shifts the binary representation of the value by 1 to the right and assigns the resulting value to the same variable. The for loop is executed until value of variable i doesn't drop to 0.

# Q.5 What is the output of following program ?

Ans. :

```
```c
#include <stdio.h>
int main()
{
    int i = 3;
    switch (i)
    {
        case 0+1: printf("T");
            break;
        case 1+2: printf("Love");
            break;
        default: printf("India");
    }
    return 0;
}
```
```

Program outputs 'Love'. The given expression gets evaluated in cases. The control goes to the second case block after evaluating 1 + 2 = 3.

# Long Answered Questions

+   Q.1 What is a control statement ? (Refer section 4.1)
+   Q.2 Discuss various condition checking statements provided by C#. (Refer section 4.1)
+   Q.3 What is use of break and continue ? (Refer section 4.4)
+   Q.4 What is necessary for any looping statement ? (Refer section 4.3)
+   Q.5 What is the purpose of using statement ? (Refer section 4.5)
+   Q.6 Write a C# program to check whether the entered year is a Leap year or not.

AU : May-18, Marks 5

Ans. :

```
```csharp
/* Program to check whether the entered year is Leap year or not*/
using System;
namespace CheckLeapYear
{
    class Program
    {
        static void Main(string[] args)
        {
```
```
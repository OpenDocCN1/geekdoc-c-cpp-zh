```
Console.WriteLine('Enter Year :');
int Year = int.Parse(Console.ReadLine());
if (((Year % 4 == 0) && (Year % 100 != 0)) || (Year % 400 == 0)) Console.WriteLine("{0} is a Leap Year.", Year);
else Console.WriteLine("{0} is not a Leap Year.", Year);
Console.ReadLine();
}
}
```

# Q.7 Write a C# program to Get a Number and Display the Number in its Reverse order.

AU : Dec.-18, Marks 7

Ans. :

```
/* C# program to reverse a number */
using System;
namespace ReverseNo
{
class Program
{
static void Main(string[] args)
{
Console.WriteLine("Enter a No. to reverse");
int Number = int.Parse(Console.ReadLine());
int Reverse = 0;
while(Number>0)
{
int remainder = Number % 10;
Reverse = (Reverse * 10) + remainder;
Number = Number / 10;
}
Console.WriteLine("Reverse No. is {0}",Reverse);
Console.ReadLine();
}
}
}
```

# Q.8 Write a C# program to Sort a List of Names in Alphabetical Order.

AU : Dec.-18, Marks 6

Ans. :

```
/*
 * C# Program to Sort a List of Names in Alphabetical Order
 */
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
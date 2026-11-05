```
Console.WriteLine("Good");
break;
case A+:
    Console.WriteLine("Excellent");
    break;
    default:
        Console.WriteLine("No matching grade");
        break;
    }
    Console.WriteLine("Grade is {0}",grade);
    Console.ReadLine();
}
```

# Example 12:

```
using System;
namespace nestedswitch
{
    class Program
    {
        static void Main(string[] args)
        {
            int x = 20;
            int y = 40;

            switch(x)
            {
                case 20:
                    Console.WriteLine("Part of outer switch");
                    switch(y)
                    {
                        case 40:
                            Console.WriteLine("Part of inner switch");
                            break;
                    }
                    break;
            }
            Console.WriteLine("Value of x is :{0}",x);
            Console.WriteLine("Value of y is: {0}",y);
            Console.Read();
        }
    }
}
```
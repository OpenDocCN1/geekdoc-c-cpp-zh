# Part I: C# Fundamentals

Suppose that you want to add some debugging statements to the program so that you can print out the intermediate results. The additional lines of code are highlighted:

```
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace TestDefine
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.Write("Please enter a number: ");
            int num = int.Parse(Console.ReadLine());
            int sum = 0;
            for (int i = 1; i <= num; i++)
            {
                //---sum up all odd numbers---
                if (i % 2 == 1)
                {
                    sum += i;
                    Console.WriteLine("i={0}, sum={1}", i, sum);
                }
            }
            Console.WriteLine(
                "Sum of all odd numbers from 1 to {0} is {1}",
                num, sum);
            Console.ReadLine();
        }
    }
}
```
```

You do not want the debugging statements to be included in the production code so you first define a symbol (such as DEBUG) using the #define preprocessor directive and wrap the debugging statements with the #if and #endif preprocessor directives:

```
```csharp
#define DEBUG
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace TestDefine
{
    class Program
    {
        static void Main(string[] args)
        {
```
```
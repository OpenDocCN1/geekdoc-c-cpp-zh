# 9.5 Foreach loop

This loop is specifically designed to iterate through all elements of an array. It is great for retrieving elements of an array efficiently.

**Syntax:**

```
foreach(type identifier in expression)
    statement – block
```

**Example:**

```
```csharp
using System;
namespace arraydeclare
{
    class Arraydemo
    {
        static void Main(string[] args)
        {
            int [] a = new int[5];

            for(int x = 0;x < 5;x++)
            {
                a[x] = x + 10;
            }
            foreach(int y in a)
            {
                int x = y - 10;
                Console.WriteLine("Element[{0}]={1}", x,y);
                x++;
            }
            Console.ReadLine();
        }
    }
}
```
```

The code is compiled and executed, the output is:

```
Element [0] = 10
Element [1] = 11
Element [2] = 12
```
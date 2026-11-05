# Example

```
// Illustration of for each loop
using System;
namespace CSharpIteration
{
class foreachloop
{
static void Main()
{
int[] intarr = { 100, 200, 300, 400, 500 };
foreach(int cnt in intarr)
{
Console.WriteLine("" + cnt);
}
Console.ReadLine();
}
}
}
```

Input

# Output

```
100
200
300
400
500
```

# 4.3.5 Nested Loop

# Concept

+   1. When one loop is used inside the other loop that is known as nested loop.

# Explanation

+   2. One can use for loop inside while loop, do-while loop inside for loop, while loop inside while loop or so on.
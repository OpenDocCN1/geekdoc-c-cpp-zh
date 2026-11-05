# Example

```
```csharp
//Illustration of thread Abort operation
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;

namespace MultiThread
{
class AbortOp
{
static void Main(string[] args)
{
Thread th = new Thread(Show);

if (th.IsAlive)
{
th.Start();
th.Abort(); //show method if immediately stopped as thread aborts
}
for (int cnt = 1; cnt <= 10; cnt ++)
{
Console.WriteLine("India");
}
}
private static void Show()
{
for (int cnt = 1; cnt <= 5; cnt ++)
{
Console.WriteLine("Welcome To");
}
}
}
}
```
```

# Output

India
India
India
India
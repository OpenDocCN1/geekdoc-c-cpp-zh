forgotten, C# provides a special keyword to handle this locking synchronization pattern. Listing 20.4 demonstrates the use of the lock keyword, and Output 20.3 shows the results.

# LISTING 20.4: Synchronization Using the lock Keyword

```
using System; using System.Threading; using System.Threading.Tasks;
public class Program
{
readonly static object _Sync = new object();
const int _Total = int.MaxValue;
static long _Count = 0;

public static void Main()
{
// Use Task.Factory.StartNew for .NET 4.0
Task task = Task.Run(() => Decrement());

// Increment
for(int i = 0; i < _Total; i++)
{
lock(_Sync)
{
_Count++;
}
}

task.Wait();
Console.WriteLine($"Count = {_Count}");
}

static void Decrement()
{
for(int i = 0; i < _Total; i++)
{
lock(_Sync)
{
_Count--;
}
}
}
}
```

# OUTPUT 20.3

Count = 0
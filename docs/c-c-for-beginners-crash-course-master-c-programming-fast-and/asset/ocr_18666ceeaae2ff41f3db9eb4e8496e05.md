# Example of while loop

# Example 13:

```
```csharp
using System;
namespace whileloop
{
    class Program
    {
        static void Main(string[] args)
        {
            int var;
            var=50;
            while(var<150)
            {
                Console.WriteLine("Value of variable is:{0}",var);
                var=var+10;
            }
        }
    }
}
```
```

In the preceding code, the variable var is initialized with value 50. The while loop checks for the condition. If the condition is less than 150, the statements inside the loop are executed. If false, the control does not enter the while loop.
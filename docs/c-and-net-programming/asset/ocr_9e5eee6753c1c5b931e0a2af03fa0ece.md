# 4. While loop syntax

# Syntax

```
```csharp
Initialization;
while(condition)
{
    Body of while loop
}
```
```

5. Body of while loop repeatedly executes as long as condition is true. When the condition becomes false the program control shifts to the statements present just after the while loop.

# Example

```
```csharp
// Illustration of while loop

using System;
namespace CSharpIteration
{
    class whileLoop
    {
        static void Main()
        {
            int cnt = 1;
            while (cnt <= 10)
            {
                Console.WriteLine(cnt);
                Console.WriteLine("");
                cnt++;
            }
            Console.ReadLine();
        }
    }
}
```
```

| Input nil | Output |
|---|---|
|  | 1 |
|  | 2 |
|  | 3 |
|  | 4 |
|  | 5 |
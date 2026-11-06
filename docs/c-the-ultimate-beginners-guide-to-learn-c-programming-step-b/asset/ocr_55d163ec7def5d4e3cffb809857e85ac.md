```
```csharp
Console.ReadLine();
}
}
}
```
```

The code returns the following output:

```
x is less than 10
The value of x is : 5
```

The condition was found to be true, that is, the value of variable x is less than 10, hence, and the statement just below the condition was executed. What if the condition was false?

```
```csharp
using System;

namespace DecisionMaking {
    class IfStatement {
        static void Main(string[] args) {

            /* defining a local variable */
            int x = 15;

            /* check a boolean condition via if statement */
            if (x < 10) {

                /* to be printed of the condition is true */
                Console.WriteLine("x is less than 10");
            }
            Console.WriteLine("The value of x is : {0}", x);
            Console.ReadLine();
        }
    }
}
```
```

The code returns the following:

```
The value of x is : 15
```

The condition was found to be false, hence the statement outside its block was
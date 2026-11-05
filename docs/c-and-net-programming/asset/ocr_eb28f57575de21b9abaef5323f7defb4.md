```
th.Start();
for (int cnt = 1; cnt <= 10; cnt ++)
{
    Console.WriteLine("India");
}
}

private static void Show()
{
    for (int cnt = 1; cnt <= 5; cnt++)
    {
        Console.WriteLine("Welcome to");
    }
}
```

# Output

Welcome to
Welcome to
Welcome to
Welcome to
Welcome to
India
India
India
India
India
India
India
India
India
India

# Example

```
//illustration of thread Using With Lowest Priority
/* PrioritiesDemo2 program defines the priority. New thread has low priority therefore
method Show() of this thread gets chance after high priority Main thread. Main method
executes first. */
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
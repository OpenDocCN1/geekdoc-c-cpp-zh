```
/* if the condition is true, check the if condition below */
if (y == 2) {
    /* if the condition is true, print the following */
    Console.WriteLine("Value of x is 1 and b is 2");
}
}
Console.WriteLine("Exact value of x is : {0}", x);
Console.WriteLine("Exact value of y is : {0}", y);
Console.ReadLine();
}
}
}
```

The code returns:

```
Value of x is 1 and b is 2
Exact value of x is : 1
Exact value of y is : 1
```

Both *if* conditions evaluated to a true, hence the statement within the nested *if* were executed. If either or both conditions evaluated to a false, then this statement could not have been executed. Here is an example:

```
using System;

namespace DecisionMaking {
    class NestedIf {
        static void Main(string[] args) {
            /* defining local variables */
            int x = 1;
            int y = 2;
            /* checking the boolean condition */
            if (x == 1) {
                /* if the condition is true, check the if condition below */
```
```
case <value_N>
    // code
    break;

default
    // code
    break;
}
```

Here is an example:

```
using System;

public class SwitchStatement
{
    public static void Main()
    {
        int a = 3;
        switch (a)
        {
            case 1:
                Console.WriteLine("The value of x is 1");
                break;

            case 2:
                Console.WriteLine("The value of x is 2");
                break;

            case 3:
                Console.WriteLine("The value of x is 3");
                break;

            default:
                Console.WriteLine("Unknown value of x");
```
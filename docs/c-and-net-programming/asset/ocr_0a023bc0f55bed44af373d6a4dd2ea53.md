..........
..........

# Example

// Illustration of goto statement in which control is transferred to the 'stop' label in the fourth iteration of the loop

```
using System;
namespace CSharpJump
{
class gotostatement
{
    static void Main()
    {
        int cnt;
        for (cnt = 1; cnt <= 5; cnt++)
        {
            Console.WriteLine("" + cnt);
            if (cnt%4 == 0)
            {
                goto stop;
            }
        }

        stop:
        Console.WriteLine("Loop Stops");
        Console.ReadLine();
    }
}
}
```

Input Nil

# Output

```
1
2
3
4

Loop Stops
```
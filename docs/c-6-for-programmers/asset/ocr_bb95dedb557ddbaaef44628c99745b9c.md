```
// Fig. 7.14: CalculatePowers.cs
// Optional parameter demonstration with method Power.
using System;

class CalculatePowers
{
    // call Power with and without optional arguments
    static void Main()
    {
        Console.WriteLine($"Power(10) = {Power(10)}");
        Console.WriteLine($"Power(2, 10) = {Power(2, 10)}");
    }

    // use iteration to calculate power
    static int Power(int baseValue, int exponentValue = 2)
    {
        int result = 1;

        for (int i = 1; i <= exponentValue; ++i)
        {
            result *= baseValue;
        }

        return result;
    }
}
```

Power(10) = 100
Power(2, 10) = 1024

Fig. 7.14 | Optional parameter demonstration with method Power.

# 7.14 Named Parameters

Normally, when calling a method, the argument values—in order—are assigned to the parameters from left to right in the parameter list. Consider a Time class that stores the time of day in 24-hour clock format as int values representing the hour (0–23), minute (0–59) and second (0–59). Such a class might provide a SetTime method with optional parameters like

```
public void SetTime(int hour = 0, int minute = 0, int second = 0)
```

In the preceding method header, all three of SetTime's parameters are optional. Assuming that we have a Time object named t, consider the following calls to SetTime:

+   - t.SetTime()—This call specifies no arguments, so the compiler assigns the default value 0 to each parameter. The resulting time is 12:00:00 AM.
+   - t.SetTime(12)—This call specifies the argument 12 for the first parameter, hour, and the compiler assigns the default value 0 to the minute and second parameters. The resulting time is 12:00 PM.
+   - t.SetTime(12, 30)—This call specifies the arguments 12 and 30 for the parameters hour and minute, respectively, and the compiler assigns the default value 0 to the parameter second. The resulting time is 12:30:00 PM.
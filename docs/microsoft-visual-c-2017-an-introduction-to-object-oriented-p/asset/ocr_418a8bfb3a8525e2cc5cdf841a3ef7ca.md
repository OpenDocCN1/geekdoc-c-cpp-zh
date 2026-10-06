# Understanding Exceptions

```
using System;
using static System.Console;
class MilesPerGallon
{
    static void Main()
    {
        int milesDriven;
        int gallonsOfGas;
        int mpg;
        Write("Enter miles driven ");
        milesDriven = Convert.ToInt32(ReadLine());
        Write("Enter gallons of gas purchased ");
        gallonsOfGas = Convert.ToInt32(ReadLine());
        mpg = milesDriven / gallonsOfGas;
        WriteLine("You got {0} miles per gallon", mpg);
    }
}
```

**Figure 11-1** The MilesPerGallon program

| Enter miles driven 300
Enter gallons of gas purchased 12
nYou got 25 miles per gallon |

| Enter miles driven 300
Enter gallons of gas purchased 0
Unhandled Exception: System.DivideByZeroException: Attempted to divide by zero.
at MilesPerGallon.Main() |

**Figure 11-2** Two executions of the MilesPerGallon program, a dialog box reports that the application has stopped working and needs to close. Because this error is intentional for demonstration purposes, you can ignore the message by clicking the Close button in the lower-right corner of the dialog box.

![](bbox=[0.102, 0.693, 0.158, 0.728])

In the first execution of the MilesPerGallon program in Figure 11-2, the user entered two usable integers, and division was carried out successfully. However, in the second execution, the user entered 0 for gallons of gas, and the error message indicates that an unhandled exception named **System.DivideByZeroException** was created. The message gives further information("Attempted to divide by zero.") and shows the method where the exception occurred—in **MilesPerGallon.Main()**
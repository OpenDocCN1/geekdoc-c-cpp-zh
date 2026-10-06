```
using System;
using static System.Console;
class MilesPerGallon4
{
    static void Main()
    {
        int milesDriven;
        int gallonsOfGas;
        int mpg;
        try
        {
            Write("Enter miles driven");
            milesDriven = Convert.ToInt32(ReadLine());
            Write("Enter gallons of gas purchased");
            gallonsOfGas = Convert.ToInt32(ReadLine());
            mpg = milesDriven / gallonsOfGas;
        }
        catch (Exception e)
        {
            mpg = 0;
            WriteLine(e.message);
        }
        WriteLine("You got {0} miles per gallon", mpg);
    }
}
```

# Figure 11-10 The MilesPerGallon4 program

```
Enter miles driven 250
Enter gallons of gas purchased 0
Attempted to divide by zero.
Youou got 0 miles per gallon
```

# Figure 11-11 Execution of the MilesPerGallon4 program
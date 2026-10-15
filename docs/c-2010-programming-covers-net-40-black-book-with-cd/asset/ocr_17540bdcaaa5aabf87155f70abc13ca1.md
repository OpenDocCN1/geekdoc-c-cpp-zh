![](bbox=[0.16, 0.07, 0.77, 0.33])

# Figure 2.2: Showing the New Console Application

8. Add the code given in Listing 2.6 to the Program.cs file of your application:

# Listing 2.6: Showing the Code of the Program.cs File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace DeclaringVariable
{
    class Program
    {
        static void Main(string[] args)
        {
            short x;    //Declaring short type variable
            int y;      //Declaring integer type variable
            double z;   //Declaring double type variable
            x = 6;
            y = 10;
            z = x + y;
            Console.WriteLine("x = {0}, Y = {1}, Z = {2}", x, y, z);
            Console.ReadLine();
        }
    }
}
```

In Listing 2.6, we have declared some variables, assigned values to them, and then print the result. We have called the WriteLine() method of the System.Console object to display the values of the variables. The output of Listing 2.6 is shown in Figure 2.3:

![](bbox=[0.33, 0.76, 0.62, 0.84])

# Figure 2.3: Displaying the Output of DeclaringVariable Application

# Initializing Variables

After creating a variable, you must initialize it with some value. Variables can be initialized in several ways—at the time they are declared, within the application with a fixed value, or by copying the value of another variable
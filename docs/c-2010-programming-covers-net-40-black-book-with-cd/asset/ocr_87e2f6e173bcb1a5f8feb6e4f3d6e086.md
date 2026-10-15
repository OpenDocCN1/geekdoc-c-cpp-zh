```
bool check = dynBool;
DateTime date = dynDate;

//Printing the values
Console.WriteLine("\nDouble: "+d);
Console.WriteLine("String: "+str);
Console.WriteLine("Boolean: "+check);
Console.WriteLine("DateTime: "+date);
}

static void Main(string[] args)
{
    Program p = new Program();
    p.Method1();
    p.Method2();
    Console.WriteLine("\n");
    Console.WriteLine("Press Enter to quit....");
    Console.Read();
}
}
```

In Listing 7.3, we declare and assign values to four dynamic data type variables. The p object calls the Method1 method, which prints the data types of these variables. The dynamic data types implicitly select the data types according to the values assigned to them and print those values on the console screen. Next, the p object calls the Method2 method, which takes the values for different variables from respective dynamic variables and prints the values.

The output of Listing 7.3 is shown in Figure 7.5:

![](bbox=[0.12, 0.48, 0.89, 0.64])

Let’s now learn how to use ExpandoObject classes.

# Using the ExpandoObject Class

The instance of the ExpandoObject class that is passed as a parameter is treated as dynamic objects in C#. This indicates that the IntelliSense does not work for object members; therefore, the compiler does not raise any errors when non-existent members are called. However, an exception occurs at run time when a non-existing member is called in the program. Let’s create a Console application, named UsingExpandoObject (also available on the CD), which creates and uses a method to print the names and values of different properties. Listing 7.4 shows the code of the UsingExpandoObject application:

Listing 7.4: Showing an Example of the ExpandoObject Class

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Dynamic;
```
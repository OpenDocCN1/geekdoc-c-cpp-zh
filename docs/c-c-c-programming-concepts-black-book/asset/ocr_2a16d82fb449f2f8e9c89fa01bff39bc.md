# *Named Arguments*

Named arguments are useful when a method holds quite a number of arguments. In this case, when we try to call this method, we may forget the order in which they appear. Therefore, the use of named arguments helps in remembering the order in which the arguments in the method appear. Listing 17.56 shows a simple example of named arguments:

Listing 17.56: Showing an Example of Named Arguments

```
```csharp
using System;
class Program
{
    public static void Main()
    {
        //calculating Area normally
        Console.WriteLine(CalculateArea(100, 20));
        //calculating area using named arguments
        Console.WriteLine(CalculateArea(length:100, width:20));
        //shuffling the position of the named arguments
        Console.WriteLine(CalculateArea(width:20, length:100));
        //combining both positional and named arguments
        Console.WriteLine(CalculateArea(100, width:20));
    }
    public static int CalculateArea(int length, int width)
    {
        return (breadth * width);
    }
}
```
```

In the preceding program, we have declared a method named CalculateArea, which calculates the area using the length and width of an object. In the Main() method, we have first called this method by providing the values of length and width at the exact places that are referred to as positional arguments. Then, we have specified the name of the arguments along with their values, which implement the named arguments. Next, we have again called the same method by just shuffling the position of the named arguments and at last, we have called the method by providing both positional and named arguments. In these four cases, the output will be same.

# *Optional Arguments*

Optional arguments are used in case where a method contains some of the arguments that will be used optionally in few places in a program. These optional arguments may hold a constant value or a default value type so that, whenever the values are not specified, the execution will be carried out using the default or constant values. Listing 17.57 shows an example of optional arguments:

Listing 17.57: Showing an Example of Optional Arguments

```
```csharp
using System;
class Employee
{
    public static void Main()
    {
        //Providing positional arguments
        Print(100, "Mr. A Roy", "Manager");
        //Using optional arguments
        Print(200, "Mr. J Sen");
    }
    public static void Print(int id, string name, string designation = "Member", long salary=10000)
```
```
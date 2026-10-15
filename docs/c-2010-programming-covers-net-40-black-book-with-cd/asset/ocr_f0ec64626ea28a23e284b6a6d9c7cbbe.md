```
{
    Console.WriteLine(*(ptr + i));
}
}
class MainClass
{
    public static void Main()
    {
        MyClass myclass = new MyClass();
        myclass.MyMethod();
        Console.WriteLine("\n");
        Console.WriteLine("Press ENTER to quit...");
        Console.Read();
    }
}
```

In Listing 6.3, we have created an integer array named MyArray[] and a pointer variable named MyPointer through which we can access the elements of MyArray[] array.

Figure 6.5 shows the output of the preceding code:

![](bbox=[0.25, 0.33, 0.68, 0.5])

Figure 6.5: Showing the Output of the PointertoArray Application

Let’s now learn to use pointers to structures.

# Using Pointers to Structures

The pointers can be used with a structure if the structure contains only value types as its members. Pointers can access the members of a structure by using the pointer operator (->). Let’s create a Console application, named PointersToStruct (also available in the CD), which shows how to use pointers to access structures. Listing 6.4 shows the code of the Program.cs file of the PointersToStruct application:

Listing 6.4: Showing the Code of the Program.cs File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace PointersToStruct
{
struct MyStruct {
    public double Length;
    public double Breadth;
    public double Height;
    public void SetDimensions()
    {
        Console.Write("Enter Length of Room (in meter):");
        Length = Convert.ToDouble(Console.ReadLine());
        Console.Write("Enter Breadth of Room (in meter):");
        Breadth = Convert.ToDouble(Console.ReadLine());
        Console.Write("Enter Height of Room (in meter):");
        Height = Convert.ToDouble(Console.ReadLine());
    }
    public void ShowVolume()
```
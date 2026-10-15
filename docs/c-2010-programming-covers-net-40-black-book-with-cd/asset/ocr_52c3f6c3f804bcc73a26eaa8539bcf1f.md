# Immediate Solutions

# Creating Pointer to int Data Type

Pointers are the variables that hold the address of other variables of value types, such as int and char. Let’s create a Console application, named MyPointer (also available in the CD ), which shows how to create a pointer to int data type. Listing 6.1 shows the code of the Program.cs file of the MyPointer application:

# Listing 6.1: Creating Pointer to int Data Type

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MyPointer {
class Program {
    unsafe static void Main(string[] args) {
        int Number = 100;
        int* MyPointer;
        MyPointer = &Number;
        {
        Console.WriteLine("The value of 'Number' is: "+Number);
        Console.WriteLine("The value of 'MyPointer' is: "+(int)MyPointer);
        Console.WriteLine("\n");
        Console.WriteLine("Press ENTER to quit.....");
        Console.Read();
        }
    }
}
```

In Listing 6.1, we have created an integer pointer MyPointer that holds the memory address of an integer variable named as Number.

To execute any application containing pointers, first you need to change the settings in the Visual Studio 2010. To do this, perform the following steps:

+   1. Select and right-click the project name, which in this case is MyPointer, in Solution Explorer and select the Properties option from the context menu.

The MyPointer properties window appears, as shown in Figure 6.1:

![](bbox=[0.24, 0.605, 0.795, 0.907])

Figure 6.1: Showing the MyPointer Properties Window
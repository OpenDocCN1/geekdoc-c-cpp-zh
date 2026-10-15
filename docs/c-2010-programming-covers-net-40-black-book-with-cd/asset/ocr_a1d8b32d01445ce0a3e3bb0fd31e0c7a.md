```
unsafe static void Main(string[] args)
{
    int Number = 100;
    int* MyPointer;
    MyPointer = &Number;
    Console.WriteLine("Old values:");
    Console.WriteLine("Number: " + Number);
    Console.WriteLine("MyPointer: " + (int)MyPointer);
    Console.WriteLine("*MyPointer: " + *MyPointer);
    *MyPointer = 50;
    Console.WriteLine("--------------------------");
    Console.WriteLine("New values:");
    Console.WriteLine("Number: " + Number);
    Console.WriteLine("MyPointer: " + (int)MyPointer);
    Console.WriteLine("*MyPointer: " + *MyPointer);
    Console.Read();
}
```

In Listing 6.2, you can see that the pointer variable *MyPointer holds the value, which is on the memory address held by &MyPointer.

Figure 6.4 shows the output of the preceding code:

![](bbox=[0.3, 0.35, 0.78, 0.48])

Figure 6.4: Dereferencing Pointers

NOTE
Every time we execute the application, the value of pointer changes on the system.

Let’s now learn to use pointers to arrays.

# Using Pointers to Arrays

In C#, you can access array elements by using pointers. Let’s create a Console application, named PointersToArray (also available in the CD), which shows how to access the elements of an array by using pointers. Listing 6.3 shows the code of the Program.cs file of the PointersToArray application:

Listing 6.3: Showing the Code of the Program.cs File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace PointerToArray
{
    class MyClass
    {
        public unsafe void MyMethod()
        {
            int[] MyArray = new int[10];
            for (int Counter = 0; Counter < 10; Counter++)
            {
                MyArray[Counter] = Counter * Counter;
            }
            fixed (int* MyPointer = MyArray)
            ShowData(MyPointer);
        }
        public unsafe void ShowData(int* ptr)
        {
            for (int i = 0; i < 10; i++)
```
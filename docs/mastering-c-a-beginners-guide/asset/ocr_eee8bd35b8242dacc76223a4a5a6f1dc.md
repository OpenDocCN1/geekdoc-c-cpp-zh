The structure is also user defined data type, but the main difference between the arrays and Structure is that all the components of an array are of the same type. While in structure, all the components are of different data type.

# Structs with Methods

A C# Struct can also hold either static or non-static. But static methods can access only other static members, and they can’t be called by using an object of the structure. They can be included only by using the struct name. To illustrate with an example.²

```
/*Structs with Methods/Function*/
using System;
struct str
{
    int a,b;
    public void get()
    {
        Console.WriteLine("Enter a No.");
        a = Int32.Parse(Console.ReadLine());
        b = Int32.Parse(Console.ReadLine());
    }
    public void show()
    {
        int c = a + b;
        Console.WriteLine("Sum = " + c);
    }
}
```

² https://programming-incsharp.blogspot.com/2014/04/structures-and-enumerations.html, Blogspot
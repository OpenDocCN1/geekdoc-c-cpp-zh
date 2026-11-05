# 8. **Advantage of structure in C#**

+   1. Structures are stored on the stack, so there are some advantage of structures, like, structure are created more quickly than heap –allocated objects.
+   2. Structures are automatically deallocated, when goes out of the scope.
+   3. Structures are value type so that one can easily copy value type variables on the stack memory.

# 9. **When to prefer structure over class**

Structure is preferred only in case,

+   1. It represents a single value.
+   2. Its size is smaller than 16 byte.
+   3. It is immutable.
+   4. It is required for boxing.

# **Example**

```
```csharp
//illustration of structure and its properties and constructor
using System;
namespace StructureDemo
{
    class StructRect
    {
        struct Rectangle
        {
            int len,brd;
            public rectangle(int l, int b)    //Constructor
            {
                len = l;
                brd = b;
            }
            public void GetArea()             // method
            {
                Console.WriteLine("Area of rectangle is - ");
                Console.WriteLine(len*brd);
            }
        }
        static void Main(string[] args)
        {
            Rectangle rect1 = new Rectangle(25,40);
            rect1.GetArea();
            Console.ReadLine();
        }
    }
}
Input nil
```
```
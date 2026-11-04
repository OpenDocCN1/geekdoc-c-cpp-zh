# stackalloc

You can allocate memory from the stack by using **stackalloc**. It can be used only when initializing local variables and has this general form:

```
type *p = stackalloc type[size]
```

Here, *p* is a pointer that receives the address of the memory that is large enough to hold *size* number of objects of *type*. Also, *type* must be a nonreference type. If there is not room on the stack to allocate the memory, a **System.StackOverflowException** is thrown. Finally, **stackalloc** can be used only in an unsafe context.

Normally, memory for objects is allocated from the *heap*, which is a region of free memory. Allocating memory from the stack is the exception. Variables allocated on the stack are not garbage-collected. Rather, they exist only while the method in which they are declared is executing. When the method is left, the memory is freed. One advantage to using **stackalloc** is that you don't need to worry about the memory being moved about by the garbage collector.

Here is an example that uses **stackalloc**:

```
// Demonstrate stackalloc.

using System;

class UseStackalloc {
    unsafe static void Main() {
        int* ptrs = stackalloc int[3];

        ptrs[0] = 1;
        ptrs[1] = 2;
        ptrs[2] = 3;

        for(int i=0; i < 3; i++)
            Console.WriteLine(ptrs[i]);
    }
}
```

The output is shown here:

```
1
2
3
```

# Creating Fixed-Size Buffers

There is a second use of the **fixed** keyword that enables you to create fixed-sized, single-dimensional arrays. In the C# documentation, these are referred to as *fixed-size buffers*. A fixed-size buffer is always a member of a **struct**. The purpose of a fixed-size buffer is to allow the creation of a **struct** in which the array elements that make up the buffer are contained within the **struct**. Normally, when you include an array member in a **struct**, only a reference to the array is actually held within the **struct**. By using a fixed-size buffer, you cause the entire array to be contained within the **struct**. This results in a structure that can be used in situations in which the size of a **struct** is important, such as in mixed-language programming, interfacing to data not created by a C# program, or whenever a nonmanaged **struct** containing an array is required. Fixed-size buffers can be used only within an unsafe context.
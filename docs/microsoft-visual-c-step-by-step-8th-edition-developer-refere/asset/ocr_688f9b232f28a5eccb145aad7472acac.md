January and February are written to the console.

Notice that performing a mathematical operation (such as the increment operation) on an enumeration variable changes the internal integer value of the variable. When the variable is written to the console, the corresponding enumeration value is displayed.

11. Press Enter to close the program and return to the Visual Studio 2015 programming environment.

12. Modify the first statement in the doWork method to initialize the first variable to Month.December, as shown in bold here:

Click here to view code image

```
static void doWork()
{
    Month first = Month.December;
    Console.WriteLine(first);
    first++;
    Console.WriteLine(first);
}
```

13. On the Debug menu, click Start Without Debugging.

Visual Studio 2015 builds and runs the program. This time, the word December is written to the console, followed by the number 12.

![](bbox=[0.35, 0.5, 0.66, 0.6])

Although you can perform arithmetic on an enumeration, if the results of the operation are outside the range of values defined for the enumeration, all the runtime can do is interpret the value of the variable as the corresponding integer value.

14. Press Enter to close the program and return to the Visual Studio 2015 programming environment.

# Working with structures

Chapter 8 illustrated that classes define reference types that are always created on the heap. In some cases, the class can contain so little data that the overhead of managing the heap becomes disproportionate. In these cases, it is better to define the type as a structure. A structure is a value type. Because structures are stored on the stack, as long as the structure is reasonably small, the memory management overhead is often reduced.

Like a class, a structure can have its own fields, methods, and (with one important exception discussed later in this chapter) constructors.
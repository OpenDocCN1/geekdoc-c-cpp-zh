we look at boxing and the cost of transitioning between value types and reference types. The difference between value types and reference types is an underlying implementation difference:

+   Value types represent simple data storage located on the stack. The stack is used for items of a known size, so items on the stack can be retrieved faster than those on the managed heap.

+   Reference types are based on complex classes with implementation inheritance from their parent classes, and custom storage on the managed heap. The managed heap is optimized to support dynamic allocation of differently sized objects.

Note that the two implementations are stored in different portions of memory. As a result, value types and reference types are treated differently within assignment statements, and their memory management is handled differently. It is important to understand how these differences affect the software you will write in Visual Basic. Understanding the foundations of how data is manipulated in the .NET Framework will enable you to build more reliable and better-performing applications.

Consider the difference between the stack and the heap. The stack is a comparatively small memory area in which processes and threads store data of fixed size. An integer or decimal value needs the same number of bytes to store data, regardless of the actual value. This means that the location of such variables on the stack can be efficiently determined. (When a process needs to retrieve a variable, it has to search the stack. If the stack contained variables that had dynamic memory sizes, then such a search could take a long time.)

Reference types do not have a fixed size — a string can vary in size from two bytes to nearly all the memory available on a system. The dynamic size of reference types means that the data they contain is stored on the heap, rather than the stack. However, the address of the reference type (that is, the location of the data on the heap) does have a fixed size, and thus can be (and, in fact, is) stored on the stack. By storing a reference only to a custom allocation on the stack, the program as a whole runs much more quickly, as the process can rapidly locate the data associated with a variable.

Storing the data contained in fixed and dynamically sized variables in different places results in differences in the way variables behave. Rather than limit this discussion to the most basic of types in .NET, this difference can be illustrated by comparing the behavior of the System.Drawing.Point structure (a value type) and the System.Text.StringBuilder class (a reference type).

The Point structure is used as part of the .NET graphics library, which is part of the System.Drawing namespace. The StringBuilder class is part of the System.Text namespace and is used to improve performance when you're editing strings.

First, let's examine how the System.Drawing.Point structure is used. To do this, you'll create a new method called ValueType() within your ProVB_VS2010 application. This new private Sub will be called from the ButtonTest click event handler. The new method will have the following format:

```
Private Sub ValueType()
    Dim ptX As System.Drawing.Point = New System.Drawing.Point(10, 20)
    Dim ptY As System.Drawing.Point
    ptY = ptX
    ptX.X = 200
    TextBox1.Text = "Pt Y = " & ptY.ToString()
End Sub
```

The output from this operation will be {[X = 10, Y = 20]}, is shown in Figure 2-2. When the code copies ptX into ptY, the data contained in ptX is copied into the location on the stack associated with ptY. Later, when the value of ptX changes, only the memory on the stack associated with ptX is altered. Altering the value of ptX has no effect on ptY. This is not the case with reference types. Consider the following code, a new method called RefType which uses the System.Text.StringBuilder class:
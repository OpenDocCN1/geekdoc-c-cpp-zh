```
swap (&x, &y);
}
Console.WriteLine($"x is now {x}, y is now {y}");
}

public static unsafe void swap(int *a, int *b)
{
    int temp;
    temp = *a;
    *a = *b;
    *b = temp;
}
```

When you compile programs containing unsafe code, you must specify the Allow Unsafe Code option when building the project. To do this, right-click the project in Solution Explorer and then click Properties. In the Properties window, click the Build tab, select Allow Unsafe Code, and then, on the File menu, click Save All.

Unsafe code also bears on how memory is managed. Objects created in unsafe code are said to be unmanaged. Although situations that require you to access memory in this way are not common, you might encounter some, especially if you are writing code that needs to perform some low-level Windows operations.

You will learn about the implications of using code that accesses unmanaged memory in more detail in Chapter 14.

# Summary

In this chapter, you learned about some important differences between value types that hold their value directly on the stack and reference types that refer indirectly to their objects on the heap. You also learned how to use the ref and out keywords on method parameters to gain access to the arguments. You saw how assigning a value (such as the int 42) to a variable of the System.Object class creates a boxed copy of the value on the heap and then causes the System.Object variable to refer to this boxed copy. You also saw how assigning a variable of a value type (such as an int) from a variable of the System.Object class copies (or unboxes) the value in the System.Object class to the memory used by the int.

+   - If you want to continue to the next chapter, keep Visual Studio 2015 running and turn to Chapter 9.
+   - If you want to exit Visual Studio 2015 now, on the File menu, click Exit. If you see a Save dialog box, click Yes and save the project.

# Quick reference
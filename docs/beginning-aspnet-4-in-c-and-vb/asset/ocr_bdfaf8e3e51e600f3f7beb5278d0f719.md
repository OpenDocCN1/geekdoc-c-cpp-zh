If you want to use an unsafe local variable, you need to declare and use it inside a method or block that is unsafe. There is one more step before you can use pointers. The C# compiler rejects unsafe code unless you tell it that your code includes unsafe blocks. The flag to do this is unsafe. Hence, to compile a file named MySource.cs that contains unsafe blocks (assuming no other compiler options), the command is this:

```
csc /unsafe MySource.cs
```

or this:

```
csc -unsafe MySource.cs
```

> > If you are using Visual Studio 2005, 2008, or 2010, you will also find the option to compile unsafe code in the Build tab of the project properties window.

# Pointer Syntax

After you have marked a block of code as unsafe, you can declare a pointer using this syntax:

```
int* pWidth, pHeight;
double* pResult;
byte*[] pFlags;
```

This code declares four variables: pWidth and pHeight are pointers to integers, pResult is a pointer to a double, and pFlags is an array of pointers to bytes. It is common practice to use the prefix p in front of names of pointer variables to indicate that they are pointers. When used in a variable declaration, the symbol * indicates that you are declaring a pointer (that is, something that stores the address of a variable of the specified type).

> > C++ developers should be aware of the syntax difference between C++ and C#. The C# statement int* pX, pY; corresponds to the C++ statement int *pX, *pY;. In C#, the * symbol is associated with the type rather than the variable name.

When you have declared variables of pointer types, you can use them in the same way as normal variables, but first you need to learn two more operators:

+   - & means take the address of, and converts a value data type to a pointer, for example int to *int. This operator is known as the address operator.
+   - * means get the content of this address, and converts a pointer to a value data type (for example, *float to float). This operator is known as the indirection operator (or sometimes as the dereference operator).

You will see from these definitions that & and * have opposite effects.
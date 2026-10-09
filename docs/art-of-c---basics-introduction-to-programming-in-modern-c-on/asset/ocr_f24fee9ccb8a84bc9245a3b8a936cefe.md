support top-level functions, and static methods are the closest thing to functions.

One another thing to note from this sample code is that namespaces are "open" in that you can use the same namespace block in multiple files (within a program). This is not true for classes, for instance. (An exception is the "partial class", and the "partial method", but we will not discuss the use of partial classes in this book.)

![](bbox=[0.11, 0.26, 0.15, 0.31])

It's not really recommended, or even necessary, to use many small files, or to put different classes in different files, etc. The code samples in this book are mainly organized for easy presentation in a book format.

# 6.2.1. Explanation

The program contains three different implementations of IsLeapYear().

In the included example of the "main" program, the first version LeapYear1.IsLeapYear() is hard-coded.

If you run the program, for example, using the dotnet CLI tool,

```
dotnet run
```

It prints out the following output to the console:

```
Is 1900 a leap year? No
Is 1984 a leap year? Yes
Is 2000 a leap year? Yes
Is 2022 a leap year? No
```

If you want to use the second version instead, for instance, then you can assign the method name, LeapYear2.IsLeapYear, to the variable isLeapYear in the beginning of the program.
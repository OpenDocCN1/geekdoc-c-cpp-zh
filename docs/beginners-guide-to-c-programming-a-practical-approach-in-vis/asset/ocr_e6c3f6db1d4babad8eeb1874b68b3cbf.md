Classes can be declared and used in C# in one of the following three ways:

+   - Declaration inside the same source code file of the program such as in Form1.cs
+   - A separate .cs file can be added to the project. The new class is then declared and coded in this file.
+   - A completely separate library file can be created in Visual Studio where the class is declared. This library file is then saved as a .dll file available for distribution and use in any C# project.

The general template of a class structure is as follows:

```
class name_of_the_class
{
    variable_type variable_1;
    variable_type variable_2;
    .
    .
    variable_type variable_n;

    return_type method_1(params_1)
    {
        method_1 code here
    }
    return_type method_2(params_2)
    {
        method_2 code here
    }
    .
    .
    .
    return_type method_m(params_m)
    {
        method_n code here
    }
}
```

Code 12.1

In this template, the class has several variables (member variables) and methods inside.
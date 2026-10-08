# 5.2 Functions

The following example shows a function header and function body:

```
int funcsort(int var1, float var2, double var3, char var4)
{
    int result;

    result = ...;

    return result;
}
```

Notice that the return-data-type is int, the function-name is funcsort, the function parameters are var1, var2, var3, and var4. The variables var1, var2, var3, and var4 are declared in the function header, are initialized by the calling routine at the time of the call, and must not be declared again. This function returns an integer value computed within the function funcsort for the variable result. The type of this variable matches the return data type.

A Simple Function The simplest one can write in C is a function that does not return any value through the return statement and does not have any arguments or parameters. Such functions can be used to output character string constants, such as printing messages, headings, and subheadings. The following sample code shows such a function:

```
void print_titles())
{
    printf("Materials Inventory of ABC Company\n\n");
    printf("Items          Unit-Cost      Total_Cost\n");
    printf("________________________________\n");

    return;
}
```

This function is called with a null list of arguments, as

```
print_titles();
```

Notice that this function has return type void, meaning that this function will not return any value through its return statement; and there is a null parameter list because the function does not need information from the calling function. A function such as this may be called anywhere in a program where titles need to be printed in the output.
# Dynamic Types

C# 2010 aims at providing the application developers more flexibility while developing applications in C#. It has introduced the new dynamic type on which, you can perform any operation, such as string manipulation or arithmetic operation. The dynamic types are resolved at runtime; therefore, you do not need to worry about the type of a variable while assigning values that are returned from methods or on evaluation of an expression. The CLR automatically performs necessary binding for you according to the data type of returned value.

Let's consider the following code snippet:

```
dynamic d = 5;
var total = d + 2;
Console.WriteLine(total);
```

In the preceding code snippet, a dynamic type variable d is declared, which has an integer value, 5. In addition, the var type variable total is used to store the sum of the value of d and 2. While declaring a variable using the var type, you do not need to define a data type for it. The CLR decides the data type for a variable of type var on the basis of the value assigned to it. The data type for a variable of type var is resolved at compile time whereas the data type for a variable of type dynamic is resolved at runtime.

Using the dynamic type, programmers can now write method and indexer calls, property and field accesses, and even object invocations, which can bypass the C# type checking process and get inferred during runtime. This feature is beneficial while working with various kinds of objects such as COM.

> Note
> The result of all the dynamic operations is also dynamic.

Next, let's learn about the support for named and optional parameters introduced in C# 2010.

# Named and Optional Arguments

C# 2010 has introduced support for named and optional arguments. These are two distinct features that have been added to C# 2010. Named arguments allow you to specify an argument for a specific parameter by associating the argument with the name of the parameter instead of passing the position of the parameter in the parameter list. On the other hand, in the optional arguments, you can omit arguments for the parameters that already have some defined default value. You can use both named and optional arguments with methods, indexers, constructors, and delegates. The evaluation of arguments takes place in the order in which they appear in the argument list and not in the order they appear in the parameter list while using both named and optional arguments.

For instance, let's consider an example where you need to perform a basic arithmetic operation, such as multiplication. In this case, you need to pass three parameters to a method called Product(), as shown in the following code snippet:

```
static int Product (int a, int b, int c = 6)
{
    return a * b * c;
}
```

The preceding code snippet shows that c is an optional parameter since a default value is specified to it inside the Product() method.

> Note
> An optional parameter must always be declared as the last parameter in the parameter list after declaring the required parameters.

You can call the Product() method without specifying the optional argument, as shown in the following code snippet:
Product (5 , 7);
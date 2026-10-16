and the last one has a value of 33:

```
TestMethod(1);
TestMethod(1, 2, 3);
```

With multiple optional parameters, the feature of named arguments shines. Using named arguments you can pass any of the optional parameters—for example, this example passes just the last one:

```
TestMethod(1, opt3: 4);
```

> **NOTE** Pay attention to versioning issues when using optional arguments. One issue is to change default values in newer versions; another issue is to change the number of arguments. It might look tempting to add another optional parameter as it is optional anyway. However, the compiler changes the calling code to fill in all the parameters, and that’s the reason earlier compiled callers fail if another parameter is added later on.

# Variable Number of Arguments

Using optional arguments, you can define a variable number of arguments. However, there’s also a different syntax that allows passing a variable number of arguments—and this syntax doesn’t have versioning issues.

Declaring the parameter of type array—the sample code uses an int array—and adding the params keyword, the method can be invoked using any number of int parameters.

```
public void AnyNumberOfArguments(params int[] data)
{
    foreach (var x in data)
    {
        WriteLine(x);
    }
}
```

> **NOTE** Arrays are explained in detail in Chapter 7, “Arrays and Tuples.”

As the parameter of the method AnyNumberOfArguments is of type int[], you can pass an int array, or because of the params keyword, you can pass one or any number of int values:

```
AnyNumberOfArguments(1);
AnyNumberOfArguments(1, 3, 5, 7, 11, 13);
```

If arguments of different types should be passed to methods, you can use an object array:

```
public void AnyNumberOfArguments(params object[] data)
{
    // etc.
```
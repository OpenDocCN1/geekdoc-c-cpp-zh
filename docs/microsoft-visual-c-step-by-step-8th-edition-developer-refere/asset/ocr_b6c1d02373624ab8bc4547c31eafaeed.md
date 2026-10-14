```
{
    int arg = 42;
    doIncrement(ref arg);    // using ref
    Console.WriteLine(arg);  // writes 43
}
```

This time, the doIncrement method receives a reference to the original argument rather than a copy, so any changes the method makes by using this reference actually change the original value. That’s why the value 43 is displayed on the console.

Remember that C# enforces the rule that you must assign a value to a variable before you can read it. This rule also applies to method arguments; you cannot pass an uninitialized value as an argument to a method even if an argument is defined as a ref argument. For example, in the following example, arg is not initialized, so this code will not compile. This failure occurs because the statement param++; within the doIncrement method is really an alias for the statement arg++;—and this operation is allowed only if arg has a defined value:

Click here to view code image

```
static void doIncrement(ref int param)
{
    param++;
}

static void Main()
{
    int arg;            // not initialized
    doIncrement(ref arg);
    Console.WriteLine(arg);
}
```

# Creating out parameters

The compiler checks whether a ref parameter has been assigned a value before calling the method. However, there might be times when you want the method itself to initialize the parameter. You can do this with the out keyword.

The out keyword is syntactically similar to the ref keyword. You can prefix a parameter with the out keyword so that the parameter becomes an alias for the argument. As when using ref, anything you do to the parameter, you also do to the original argument. When you pass an argument to an out parameter, you must also prefix the argument with the out keyword.

The keyword out is short for output. When you pass an out parameter to a method, the method must assign a value to it before it finishes or returns, as shown in the following example:

Click here to view code image

```
static void doInitialize(out int param)
{
```
a situation where you want to pass a value to, say, only the third optional parameter. With just the syntax from the previous section there is no way to do this without supplying values for the first and second optional parameters.

C# 4 also introduced named parameters that enable you to specify whichever parameters you want. This doesn't require you to do anything in particular in your method definition; it is a technique that you use when you are calling a method. The syntax is as follows:

```
MyMethod(
    <param1Name>: <param1Value>,
    ...
    <paramNName>: <paramNValue>);
```

The names of parameters are the names of the variables used in the method definition.

You can specify any number of parameters you like in this way, as long as the named parameters exist, and you can do so in any order. Named parameters can be optional as well.

You can, if you want, use named parameters for only some of the parameters in a method call. This is particularly useful when you have several optional parameters in a method signature, but some required parameters. You might specify the required parameters first, then finish off with named optional parameters. For example:

```
MyMethod(
    requiredParameter1Value,
    optionalParameter5: optionalParameter5Value);
```

If you mix named and positional parameters, though, note that you must include all positional parameters first, before the named parameters. However, you can use a different order if you prefer as long as you use named parameters throughout, as in this example:

```
MyMethod(
    optionalParameter5: optionalParameter5Value,
    requiredParameter1: requiredParameter1Value);
```

If you do this you must include values for all required parameters.

In the following Try It Out, you will see how you can use named and optional parameters.

# TRY IT OUT Using Named and Optional Parameters: Ch13Ex07

+   1. Create a new console application called Ch13Ex07 and save it in the directory C:\BegVCSharp\Chapter13.
+   2. Add a class called WordProcessor to the project and modify its code as follows:

```
public static class WordProcessor
{
    public static List<string> GetWords(
        string sentence,
        bool capitalizeWords = false,
        bool reverseOrder = false,
        bool reverseWords = false)
{
```
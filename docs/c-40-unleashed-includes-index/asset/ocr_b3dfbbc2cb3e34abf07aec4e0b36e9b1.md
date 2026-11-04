# USE OF KEYWORDS OR TYPE NAMES?

In the preceding examples, we've been using the C# keywords for primitive types, like int and decimal, to dot into static members. Alternatively, we could have used the type names that correspond with them, such as Int32 and Decimal in the System namespace. Which style to use is nothing more than a matter of user preference, and both mean exactly the same thing.

This can be confusing at first for developers with a Java background, where int and Integer have a different meaning: The former indicates a primitive value, whereas the latter is used to refer to a "boxed" reference type wrapping such a value. In .NET, the act of boxing is tied to the use of the values in relation to the object base type.

# Working with Arrays

A commonly used family of types consists of arrays, which really are a form of type constructors: given any type, you can construct an array type out of it. To facilitate certain common operations, the System.Array type exists. All arrays derive from this type, giving them some useful instance-level members and properties. For example, the rank of an array denotes the number of dimensions:

```
var xs = new int[10];
var ys = new int[3,4];
var zs = new int[3][];
```

For the first array, the rank will be 1 because there's only one dimension. The second one has a rank of 2 because of the use of the multidimensional array feature. For the last one, a jagged array, the rank of zs is still 1:

```
Console.WriteLine(xs.Rank); // 1
Console.WriteLine(ys.Rank); // 2
Console.WriteLine(zs.Rank); // 1
```

To find the range of valid indexes along the different dimensions of an array, methods such as GetLowerBound and GetUpperBound can be used. In practice, they are rarely used, in favor of for loops generating a range from zero to the array's length minus one, or a foreach loop that takes care of all the heavy lifting.

The static members on System.Array are of more interest in various circumstances. A couple of examples are shown in the following code:

```
var rnd = new Random();
var xs = new int[20];
for (int i = 0; i < 10; i++)
    xs[i] = rnd.Next(10);
```
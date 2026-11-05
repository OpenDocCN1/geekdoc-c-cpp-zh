where each argument is an expression that is implicitly convertible (§6.1) to the element type of the parameter array. In this case, the invocation creates an instance of the parameter array type with a length corresponding to the number of arguments, initializes the elements of the array instance with the given argument values, and uses the newly created array instance as the actual argument.

The expressions of an argument list are always evaluated in the order they are written. Thus the example

```
class Test
{
    static void F(int x, int y = -1, int z = -2)
    {
        System.Console.WriteLine("x = {0}, y = {1}, z = {2}", x, y, z);
    }
    static void Main()
    {
        int i = 0;
        F(i++, i++, i++);
        F(z: i++, x: i++);
    }
}
```

produces the output

x = 0, y = 1, z = 2
x = 4, y = -1, z = 3

The array covariance rules (§12.5) permit a value of an array type A[] to be a reference to an instance of an array type B[], provided an implicit reference conversion exists from B to A. Because of these rules, when an array element of a reference-type is passed as a reference or output parameter, a runtime check is required to ensure that the actual element type of the array is identical to that of the parameter. In the example

```
class Test
{
    static void F(ref object x) {...}
    static void Main()
    {
        object[] a = new object[10];
        object[] b = new string[10];
        F(ref a[0]);    // Okay
        F(ref b[1]);    // ArrayTypeMismatchException
    }
}
```

the second invocation of F causes a System.ArrayTypeMismatchException to be thrown because the actual element type of b is string and not object.
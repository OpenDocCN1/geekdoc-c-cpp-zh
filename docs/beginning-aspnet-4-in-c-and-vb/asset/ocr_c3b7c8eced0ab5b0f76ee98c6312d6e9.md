```
}
public static int GetSquareOf(int x)
{
    return x*x;
}
public static double GetPi()
{
    return 3.14159;
}
}
```

code snippet MathTest.cs

Running the MathTest example produces these results:

```
Pi is 3.14159
Square of 5 is 25
Value field of math variable contains 30
Square of 30 is 900
```

As you can see from the code, the MathTest class contains a field that contains a number, as well as a method to find the square of this number. It also contains two static methods, one to return the value of pi and one to find the square of the number passed in as a parameter.

Some features of this class are not really good examples of C# program design. For example, GetPi() would usually be implemented as a const field, but following good design here would mean using some concepts that we have not yet introduced.

# Passing Parameters to Methods

In general, parameters can be passed into methods by reference or by value. When a variable is passed by reference, the called method gets the actual variable — so any changes made to the variable inside the method persist when the method exits. But, when a variable is passed by value, the called method gets an identical copy of the variable — which means any changes made are lost when the method exits. For complex data types, passing by reference is more efficient because of the large amount of data that must be copied when passing by value.

In C#, all parameters are passed by value unless you specifically say otherwise. However, you need to be careful in understanding the implications of this for reference types. Because reference type variables hold only a reference to an object, it is this reference that will be copied, not the object itself. Hence, changes made to the underlying object will persist. Value type variables, in contrast, hold the actual data, so a copy of the data itself will be passed into the method. An int, for instance, is passed by value to a method, and any changes that the method makes to the value of that int do not change the value of the original int object. Conversely, if an array or any other reference type, such as a class, is passed into a method, and the method uses the reference to change a value in that array, the new value is reflected in the original array object.

Here is an example, ParameterTest.cs, which demonstrates the following:

```
using System;
namespace Wrox
{
    class ParameterTest
    {
        static void SomeFunction(int[] ints, int i)
        {
            ints[0] = 100;
            i = 100;
```
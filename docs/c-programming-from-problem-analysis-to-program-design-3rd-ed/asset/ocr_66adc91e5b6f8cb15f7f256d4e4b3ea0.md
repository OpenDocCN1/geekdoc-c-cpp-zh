The following are examples of valid calls to methods of the Math class:

```
double aValue = 78.926;
double result1,
result2;
result1 = Math.Floor(aValue);// result1 = 78
result2 = Math.Sqrt(aValue); // result2 = 8.88403061678651
Console.Write("aValue rounded to two decimal places"
+ " is {0}", Math.Round(aValue, 2));
```

The output for the last statement is:

aValue rounded to two decimal places is 78.93

As you look at the examples using the predefined methods from the Math class, you can see that they all have something in common. Each of the methods returns a value. Calls to methods returning values usually are placed in an expression or in an output statement. When the value is returned, there has to be a place for the value to be used.

A class can define a static method, or a class can use a static method defined in another class. If you are calling a method that is a member of the same class from where it is being called, the call statement does not have to include the class name. If you are calling a static method defined in another class, the name of the class must be included. When you use the methods in the Math class, you are using methods that are defined outside the boundaries of your class. Exp( ) is a static member of the Math class. In the following example, it returns e, the natural logarithmic base, raised to the 5th power. It is necessary to use the class name Math as a qualifier.

```
double result;
result = Math.Exp(5);
```

![](bbox=[0.22, 0.8, 0.28, 0.9])

The Math class also has two static data field members defined as constants. A call to static field members also requires prefixing the member name with the class name. Their declarations follow:

```
public const double E = 2.7182818284590452354;
public const double PI = 3.14159265358979323846;
```

An example of their use is as follows:

```
circumference = 2 * Math.PI * radius; //use of PI in an
//expression
```

Calls to value-returning methods must be placed at a location in your code where the value could be accepted when the method is finished. The call can appear anywhere a compatible value of that type can be placed. The statements in Example 3-12 on Lines 4, 6, and 9 illustrate three different places to which the static method Max( ) returns a value.
# NOTE

The Math class also has two static data field members defined as constants. A call to static field members also requires prefixing the member name with the class name. Their declarations follow:

```
public const double E = 2.7182818284590452354;
public const double PI = 3.1415926535897323846;
```

An example of their use is as follows:

```
circumference = 2 * Math.PI * radius; //use of PI in an
//expression
```

Calls to value-returning methods must be placed at a location in your code where the value could be accepted when the method is finished. The call can appear anywhere a compatible value of that type can be placed. The statements in Example 3-12 on Lines 4, 6, and 9 illustrate three different places to which the static method Max( ) returns a value.

# EXAMPLE 3.12

```
Line 1  int aValue = 200;
Line 2  int bValue = 896;
Line 3  int result;
Line 4  result = Math.Max(aValue, bValue);
// result = 896
Line 5  result += bValue *
Math.Max(aValue, bValue) - aValue;
// result = 896 + (896 * 896 - 200)
// result = 803512
Line 7  Console.WriteLine("Largest value between {0} "
Line 8  + "and {1} is {2}", aValue, bValue,
Line 9  Math.Max(aValue, bValue));
```

The output generated from Lines 7 through 9 is:

Largest value between 200 and 896 is 896

As shown in Table 3-2, the heading for Max( ) is

```
public static int Max(int, int)
```

As shown with the preceding three statements in Lines 4 through 9, values returned from a value-returning method can be returned to any location in your program where a variable of that return type can be used. The int returned in Line 4 is assigned to result. The int returned in Line 6 is used as part of an arithmetic expression. The int returned in Line 9 is an argument to the WriteLine( ) method.
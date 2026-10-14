other type, but only if the value of the argument can be converted to a double. For example, if you provide an int argument, the compiler generates code that converts the value of the argument to a double when the method is called.

# Providing built-in conversions

The built-in types have some built-in conversions. For example, as mentioned previously, an int can be implicitly converted to a double. An implicit conversion requires no special syntax and never throws an exception.

Click here to view code image

```
Example.MyDoubleMethod(42); // implicit int-to-double conversion
```

An implicit conversion is sometimes called a widening conversion because the result is wider than the original value—it contains at least as much information as the original value, and nothing is lost. In the case of int and double, the range of double is greater than that of int, and all int values have an equivalent double value. However, the converse is not true, and a double value cannot be implicitly converted to an int:

Click here to view code image

```
class Example
{
    public static void MyIntMethod(int parameter)
    {
        ...
    }
}
...
Example.MyIntMethod(42.0); // compile-time error
```

When you convert a double to an int, you run the risk of losing information, so the conversion will not be performed automatically. (Consider what would happen if the argument to MyIntMethod were 42.5. How should this be converted?) A double can be converted to an int, but the conversion requires an explicit notation (a cast):

Click here to view code image

```
Example.MyIntMethod((int)42.0);
```

An explicit conversion is sometimes called a narrowing conversion because the result is narrower than the original value (that is, it can contain less information) and can throw an OverflowException exception if the resulting value is out of the range of the target type. In C#, you can create conversion operators for your own user-defined types to control whether it is sensible to convert values to other types, and you can also specify whether these conversions are implicit or explicit.
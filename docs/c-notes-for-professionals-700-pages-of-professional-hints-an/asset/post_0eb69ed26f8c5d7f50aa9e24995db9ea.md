
> Digit to double implicit conversion called
> double to Digit implicit conversion called
> num = 7 dig2 = 12

Live Demo on .NET Fiddle

## Chapter 37: Casting

### Section 37.1: Checking compatibility without casting

If you need to know whether a value's type extends or implements a given type, but you don't want to actually cast it as that type, you can use the is operator.

```
if(value is int)
{
    Console.WriteLine(value + " is an int");
}
```

### Section 37.2: Cast an object to a base type

Given the following definitions :

```
public interface IMyInterface1
{
    string GetName();
}

public interface IMyInterface2
{
    string GetName();
}

public class MyClass : IMyInterface1, IMyInterface2
{
    string IMyInterface1.GetName()
    {
        return "IMyInterface1";
    }

    string IMyInterface2.GetName()
    {
        return "IMyInterface2";
    }
}
```

Casting an object to a base type example :

```
MyClass obj = new MyClass();

IMyInterface1 myClass1 = (IMyInterface1)obj;
IMyInterface2 myClass2 = (IMyInterface2)obj;

Console.WriteLine("I am : {0}", myClass1.GetName());
Console.WriteLine("I am : {0}", myClass2.GetName());

// Outputs :
// I am : IMyInterface1
// I am : IMyInterface2
```

### Section 37.3: Conversion Operators

In C#, types can define custom Conversion Operators, which allow values to be converted to and from other types using either explicit or implicit casts. For example, consider a class that is meant to represent a JavaScript expression:

```
public class JsExpression
{
    private readonly string expression;
    public JsExpression(string rawExpression)
    {
        this.expression = rawExpression;
    }
    public override string ToString()
    {
        return this.expression;
    }
    public JsExpression IsEqualTo(JsExpression other)
    {
        return new JsExpression("(" + this + " == " + other + ")");
    }
}
```

If we wanted to create a JsExpression representing a comparison of two JavaScript values, we could do something like this:

```
JsExpression intExpression = new JsExpression("-1");
JsExpression doubleExpression = new JsExpression("-1.0");
Console.WriteLine(intExpression.IsEqualTo(doubleExpression)); // (-1 == -1.0)
```

But we can add some explicit conversion operators to JsExpression, to allow a simple conversion when using explicit casting.

```
public static explicit operator JsExpression(int value)
{
    return new JsExpression(value.ToString());
}
public static explicit operator JsExpression(double value)
{
    return new JsExpression(value.ToString());
}

// Usage:
JsExpression intExpression = (JsExpression)(-1);
JsExpression doubleExpression = (JsExpression)(-1.0);
Console.WriteLine(intExpression.IsEqualTo(doubleExpression)); // (-1 == -1.0)
```

Or, we could change these operators to implicit to make the syntax much simpler.

```
public static implicit operator JsExpression(int value)
{
    return new JsExpression(value.ToString());
}
public static implicit operator JsExpression(double value)
{
    return new JsExpression(value.ToString());
}

// Usage:
JsExpression intExpression = -1;
Console.WriteLine(intExpression.IsEqualTo(-1.0)); // (-1 == -1.0)
```

### Section 37.4: LINQ Casting operations

Suppose you have types like the following:

```
interface IThing { }
class Thing : IThing { }
```

LINQ allows you to create a projection that changes the compile-time generic type of an IEnumerable<> via the Enumerable.Cast<>() and Enumerable.OfType<>() extension methods.

```
IEnumerable<IThing> things = new IThing[] { new Thing() }
IEnumerable<Thing> things2 = things.Cast<Thing>();
IEnumerable<Thing> things3 = things.OfType<Thing>();
```

When things2 is evaluated, the Cast<>() method will try to cast all of the values in things into Things. If it encounters a value that cannot be cast, an InvalidCastException will be thrown.

When things3 is evaluated, the OfType<>() method will do the same, except that if it encounters a value that cannot be cast, it will simply omit that value rather than throw an exception.

Due to the generic type of these methods, they cannot invoke Conversion Operators or perform numeric conversions.

```
double[] doubles = new[]{1,2,3}.Cast<double>().ToArray(); // Throws InvalidCastException
```

You can simply perform a cast inside a .Select() as a workaround:

```
double[] doubles = new[]{1,2,3}.Select(i => (double)i).ToArray();
```

### Section 37.5: Explicit Casting

If you know that a value is of a specific type, you can explicitly cast it to that type in order to use it in a context where that type is needed.

```
object value = -1;
int number = (int) value;
Console.WriteLine(Math.Abs(number));
```

If we tried passing value directly to Math.Abs(), we would get a compile-time exception because Math.Abs() doesn't have an overload that takes an object as a parameter.

If value could not be cast to an int, then the second line in this example would throw an InvalidCastException

### Section 37.6: Safe Explicit Casting (`as` operator)

If you aren't sure whether a value is of the type you think it is, you can safely cast it using the as operator. If the value is not of that type, the resulting value will be null.

```
object value = "-1";
int? number = value as int?;
if(number != null)
{
    Console.WriteLine(Math.Abs(number.Value));
}
```

Note that `null` values have no type, so the `as` keyword will safely yield `null` when casting any `null` value.

### Section 37.7: Implicit Casting

A value will automatically be cast to the appropriate type if the compiler knows that it can always be converted to that type.

```
~~~csharp
int number = -1;
object value = number;
Console.WriteLine(value);
~~~
```

In this example, we didn't need to use the typical explicit casting syntax because the compiler knows all `int`s can be cast to `objects`. In fact, we could avoid creating variables and pass `-1` directly as the argument of `Console.WriteLine()` that expects an `object`.

```
~~~csharp
Console.WriteLine( -1 );
~~~
```

### Section 37.8: Explicit Numeric Conversions

Explicit casting operators can be used to perform conversions of numeric types, even though they don't extend or implement one another.

```
~~~csharp
double value = -1.1;
int number = (int) value;
~~~
```

Note that in cases where the destination type has less precision than the original type, precision will be lost. For example, `-1.1` as a `double` value in the above example becomes `-1` as an integer value.

Also, numeric conversions rely on compile-time types, so they won't work if the numeric types have been "boxed" into objects.

```
~~~csharp
object value = -1.1;
int number = (int) value; // throws InvalidCastException
~~~
```

## Chapter 38: Nullable types

### Section 38.1: Initialising a nullable

For null values:

```
Nullable<int> i = null;
```

Or:

```
int? i = null;
```

Or:

```
var i = (int?)null;
```

For non-null values:

```
Nullable<int> i = 0;
```

Or:

```
int? i = 0;
```

### Section 38.2: Check if a Nullable has a value

```
int? i = null;
if (i != null)
{
    Console.WriteLine("i is not null");
}
else
{
    Console.WriteLine("i is null");
}
```

Which is the same as:

```
if (i.HasValue)
{
    Console.WriteLine("i is not null");
}
else
{
    Console.WriteLine("i is null");
}
```

### Section 38.3: Get the value of a nullable type

Given following nullable int

```
int? i = 10;
```

In case default value is needed, you can assign one using null coalescing operator, GetValueOrDefault method or check if nullable int HasValue before assignment.

```
```csharp
int j = i ?? 0;
int j = i.GetValueOrDefault(0);
int j = i.HasValue ? i.Value : 0;
```
```

The following usage is always unsafe. If i is null at runtime, a System.InvalidOperationException will be thrown. At design time, if a value is not set, you'll get a Use of unassigned local variable 'i' error.

```
```csharp
int j = i.Value;
```
```

### Section 38.4: Getting a default value from a nullable

The .GetValueOrDefault() method returns a value even if the .HasValue property is false (unlike the Value property, which throws an exception).

```
```csharp
class Program
{
    static void Main()
    {
        int? nullableExample = null;
        int result = nullableExample.GetValueOrDefault();
        Console.WriteLine(result); // will output the default value for int - 0
        int secondResult = nullableExample.GetValueOrDefault(1);
        Console.WriteLine(secondResult) // will output our specified default - 1
        int thirdResult = nullableExample ?? 1;
        Console.WriteLine(thirdResult) // same as the GetValueOrDefault but a bit shorter
    }
}
```
```

Output:

```
```
0
1
1
```
```

### Section 38.5: Default value of nullable types is null

```
```csharp
public class NullableTypesExample
{
    static int? _testValue;

    public static void Main()
    {
        if(_testValue == null)
            Console.WriteLine("null");
        else
            Console.WriteLine(_testValue.ToString());
    }
}
```
```

Output:

```
```
null
```
```

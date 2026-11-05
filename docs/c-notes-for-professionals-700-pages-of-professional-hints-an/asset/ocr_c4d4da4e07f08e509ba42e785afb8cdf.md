# Section 37.4: LINQ Casting operations

Suppose you have types like the following:

```
interface IThing { }
class Thing : IThing { }
```

LINQ allows you to create a projection that changes the compile-time generic type of an IEnumerable<> via the Enumerable.Cast<>() and Enumerable.OfType<>() extension methods.

```
IEnumerable<IThing> things = new IThing[] { new Thing(); }
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

# Section 37.5: Explicit Casting

If you know that a value is of a specific type, you can explicitly cast it to that type in order to use it in a context where that type is needed.

```
object value = -1;
int number = (int) value;
Console.WriteLine(Math.Abs(number));
```

If we tried passing value directly to Math.Abs(), we would get a compile-time exception because Math.Abs() doesn't have an overload that takes an object as a parameter.

If value could not be cast to an int, then the second line in this example would throw an InvalidCastException

# Section 37.6: Safe Explicit Casting (`as` operator)

If you aren't sure whether a value is of the type you think it is, you can safely cast it using the as operator. If the value is not of that type, the resulting value will be null.

```
object value = "-1";
int? number = value as int?;
if(number != null)
{
    Console.WriteLine(Math.Abs(number.Value));
}
```
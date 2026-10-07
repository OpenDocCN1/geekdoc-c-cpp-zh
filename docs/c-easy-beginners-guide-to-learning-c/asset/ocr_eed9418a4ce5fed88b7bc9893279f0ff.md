language supports the following type conversions:

# Explicit Conversion

If there is a risk of information loss, use this conversion. The fractional portion of floating-point values will disappear when you convert them to integer values (i.e., you will lose information). The conversion of a wide-range type to a narrow-range type may also result in data loss (e.g., long to int, double to float, etc.). You can complete the conversion by using the "type" operator. See the examples below:

```
class Example
{
    double yourDouble = 2.1d;
    System.Console.WriteLine(yourDouble);

    long yourLong = (long)yourDouble;
    System.Console.WriteLine(yourLong);

    yourDouble = 2e9d;
    System.Console.WriteLine(yourDouble);

    int yourInt = (int)yourDouble;
    System.Console.WriteLine(yourInt);
}
```

When you compile and run that program correctly, you will see the following results:
converting an out-of-range value to Currency are placed in a checked block in an attempt to trap negative values. Running this code produces the following output:

```
50.35
Balance is $50.35
After converting to float, = 50.35
After converting back to Currency, = $50.34
Now attempt to convert out of range value of -$50.50 to a Currency:
Result is $4294967246.00
```

This output shows that the code did not quite work as expected. First, converting back from float to Currency gave a wrong result of $50.34 instead of $50.35. Second, no exception was generated when you tried to convert an obviously out-of-range value.

The first problem is caused by rounding errors. If a cast is used to convert from a float to a uint, the computer truncates the number rather than rounds it. The computer stores numbers in binary rather than decimal, and the fraction 0.35 cannot be exactly represented as a binary fraction (just as 1/3 cannot be represented exactly as a decimal fraction; it comes out as 0.3333 recurring). The computer ends up storing a value very slightly lower than 0.35 that can be represented exactly in binary format. Multiply by 100 and you get a number fractionally less than 35, which is truncated to 34 cents. Clearly, in this situation, such errors caused by truncation are serious, and the way to avoid them is to ensure that some intelligent rounding is performed in numerical conversions instead.

Luckily, Microsoft has written a class that does this: System.Convert. The System.Convert object contains a large number of static methods to perform various numerical conversions, and the one that we want is Convert.ToUInt16. Note that the extra care taken by the System.Convert methods comes at a performance cost. You should use them only when necessary.

Let’s examine the second problem—why the expected overflow exception wasn’t thrown. The issue here is this: The place where the overflow really occurs isn’t actually in the Main routine at all—it is inside the code for the cast operator, which is called from the Main method. The code in this method was not marked as checked.

The solution is to ensure that the cast itself is computed in a checked context, too. With both this change and the fix for the first problem, the revised code for the conversion looks like the following:

```
public static explicit operator Currency (float value)
{
    checked
    {
        uint dollars = (uint)value;
        ushort cents = Convert.ToUInt16((value-dollars)*100);
        return new Currency(dollars, cents);
    }
}
```
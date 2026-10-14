method is an extension method for the int type, and another ordinary int parameter named baseToConvertTo.

The method will convert the value in i to the base indicated by baseToConvertTo. The method should return an int containing the converted value.

The ConvertToBase method should look like this:

Click here to view code image

```
static class Util
{
    public static int ConvertToBase(this int i, int baseToConvertTo)
    {
    }
}
```

4. Add an if statement to the ConvertToBase method that checks that the value of the baseToConvertTo parameter is between 2 and 10.

The algorithm used by this exercise does not work reliably outside this range of values. Throw an ArgumentException exception with a suitable message if the value of baseToConvertTo is outside this range.

The ConvertToBase method should look like this:

Click here to view code image

```
public static int ConvertToBase(this int i, int baseToConvertTo)
{
    if (baseToConvertTo < 2 || baseToConvertTo > 10)
    {
        throw new ArgumentException("Value cannot be converted to base " + baseToConvertTo.ToString());
    }
}
```

5. Add the following statements shown in bold to the ConvertToBase method, after the statement that throws the ArgumentException exception.

This code implements a well-known algorithm that converts a number from base 10 to a different number base. (Chapter 5, “Using compound assignment and iteration statements,” presents a version of this algorithm for converting a decimal number to octal.)

Click here to view code image

```
public static int ConvertToBase(this int i, int baseToConvertTo)
{
    ...
    int result = 0;
    int iterations = 0;
    do
```
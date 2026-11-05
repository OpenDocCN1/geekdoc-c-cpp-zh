+   - **ToByte:** Used for converting a type to byte
+   - **ToBoolean:** Used for converting Boolean value
+   - **ToDateTime:** Used for converting a type to the date time type
+   - **ToDouble:** Converts a type to double
+   - **ToDecimal:** Converts the floating point or integer to decimal type
+   - **ToInt64:** Converts the a type to 64 bit integer
+   - **ToSingle:** Converts the type to floating point number
+   - **ToString:** Converts the type to string type
+   - **ToUInt64:** Converts a type to an unsigned big integer

The following code snippet shows the conversion of value type to Double type.

# Example 4:

```
```csharp
using System;
namespace type
{
    class DoubleConversion
    {
        int a=10;
        float f=30.05f;
        bool b=false;

        Console.WriteLine(a.ToDouble());
        Console.WriteLine(f.ToDouble());
        Console.WriteLine(b.ToDouble());
        Console.Read();
    }
}
```
```
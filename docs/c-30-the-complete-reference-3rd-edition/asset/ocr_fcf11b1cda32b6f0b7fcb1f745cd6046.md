# # Type Conversion and Casting

In programming, it is common to assign one type of variable to another. For example, you might want to assign an int value to a float variable, as shown here:

```
```csharp
int i;
float f;

i = 10;
f = i; // assign an int to a float
```
```

When compatible types are mixed in an assignment, the value of the right side is automatically converted to the type of the left side. Thus, in the preceding fragment, the value in i is converted into a float and then assigned to f. However, because of C#'s strict type-checking, not all types are compatible, and thus, not all type conversions are implicitly allowed. For example, **bool** and **int** are not compatible. Fortunately, it is still possible to obtain a conversion between incompatible types by using a *cast*. A cast performs an explicit type conversion. Both automatic type conversion and casting are examined here.

# ## Automatic Conversions

When one type of data is assigned to another type of variable, an *implicit* type conversion will take place automatically if

+   - The two types are compatible.
+   - The destination type has a range that is greater than the source type.

When these two conditions are met, a *widening conversion* takes place. For example, the **int** type is always large enough to hold all valid **byte** values, and both **int** and **byte** are compatible integer types, so an implicit conversion can be applied.

For widening conversions, the numeric types, including integer and floating-point types, are compatible with each other. For example, the following program is perfectly valid since **long to double** is a widening conversion that is automatically performed.

```
```csharp
// Demonstrate implicit conversion from long to double.

using System;

class LtoD {
    static void Main() {
        long L;
        double D;

        L = 100123285L;
        D = L;

        Console.WriteLine("L and D: " + L + " " + D);
    }
}
```
```
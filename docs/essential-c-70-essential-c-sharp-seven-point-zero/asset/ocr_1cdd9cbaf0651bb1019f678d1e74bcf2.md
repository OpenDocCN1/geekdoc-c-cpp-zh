Ultimately, the intended recipient of the exception is the programmer writing code that calls your API—possibly incorrectly. Therefore, you should provide as much information to her that indicates both what the programmer did wrong and—perhaps more important—how to fix it. The exception type is a critical piece of the communication mechanism. There-fore, you must choose the type carefully.

# ### BEGINNER TOPIC

# #### Checked and Unchecked Conversions

As we first discussed in a Chapter 2 Advanced Topic, C# provides special key-words for marking a code block with instructions to the runtime for what should happen if the target data type is too small to contain the assigned data. By default, if the target data type cannot contain the assigned data, the data will truncate during assignment. For an example, see Listing 11.7.

```
**LISTING 11.7:** Overflowing an Integer Value
```csharp
using System;

public class Program
{
    public static void Main()
    {
        // int.MaxValue equals 2147483647
        int n = int.MaxValue;
        n = n + 1;
        System.Console.WriteLine(n);
    }
}
```
```

The results of Listing 11.7 appear in Output 11.1.

**OUTPUT 11.1**

`-2147483648`

The code in Listing 11.7 writes the value -2147483648 to the console. However, placing the code within a checked block or using the checked option when running the compiler will cause the runtime to throw an exception of type `System.OverflowException`. The syntax for a checked block uses the `checked` keyword, as shown in Listing 11.8.
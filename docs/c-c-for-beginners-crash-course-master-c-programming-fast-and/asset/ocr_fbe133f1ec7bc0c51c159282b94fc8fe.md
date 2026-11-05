```
variable_name = value;
```

The variables can be initialized in the declaration. The general form for initializing the variable is:

```
<data_type> <variable_name> = value;
```

Examples of variable initialization are:

+   - int a = 4;
+   - char z='z';
+   - double y = 12.145;

Example for demonstrating variable types:

# Example 5:

```
using System;
namespace VariableDeclare
class Program
{
    static void Main(string[] args)
    {
        int a;
        short s;
        double d;

        /*initializing variables*/
        a=20;
        s=5;
        d=a+s;
        Console.WriteLine("a={0},b={1},d={2}",a,s,d);
        Console.Read();
    }
}
```

# Accepting values from user

The Console class present in the System namespace provides ReadLine() function.
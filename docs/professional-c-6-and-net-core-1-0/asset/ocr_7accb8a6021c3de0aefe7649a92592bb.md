object, but this reference would not yet actually refer to any object. Any attempt to call a method or property against this variable would result in an error.

To instantiate a reference object in C#, you must use the `new` keyword. You create a reference as shown in the previous example and then point the reference at an object allocated on the heap using the `new` keyword:

```
objSomething = new Something();    // This creates a Something on the heap
```

# Using Type Inference

Type inference makes use of the `var` keyword. The syntax for declaring the variable changes by using the `var` keyword instead of the real type. The compiler “infers” what the type of the variable is by what the variable is initialized to. For example:

```
var someNumber = 0;
```

becomes:

```
int someNumber = 0;
```

Even though `someNumber` is never declared as being an `int`, the compiler figures this out and `someNumber` is an `int` for as long as it is in scope. Once compiled, the two preceding statements are equal.

Here is a short program to demonstrate (code file `VariablesSample/Program.cs`):

```
using static System.Console;

namespace Wrox
{
    class Program
    {
        static void Main()
        {
            var name = "Bugs Bunny";
            var age = 25;
            var isRabbit = true;
            Type nameType = name.GetType();
            Type ageType = age.GetType();
            Type isRabbitType = isRabbit.GetType();
            WriteLine($"name is type {nameType}");
            WriteLine($"age is type {ageType}");
            WriteLine($"isRabbit is type {isRabbitType}");
        }
    }
}
```

The output from this program is as follows:

```
name is type System.String
age is type System.Int32
isRabbit is type System.Bool
```

There are a few rules that you need to follow:
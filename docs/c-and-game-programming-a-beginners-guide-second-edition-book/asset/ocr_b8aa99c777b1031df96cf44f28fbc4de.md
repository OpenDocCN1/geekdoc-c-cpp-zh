# Example 1.40. Declaring and initializing variables.

```
```csharp
using System;

namespace Chapter1 {
    class Class1 {
        static void Main(string[] args) {
            int OurVariable = 1;
            Console.WriteLine("Our variable was assigned as "
                + OurVariable);
        }
    }
}
```
```

# Access Modifiers: constant, Readonly, and volatile

We can also simultaneously declare and initialize variables using the variable type constant. A constant variable cannot change its value after it has been specified (this is also true for the readonly modifier). Declaring a constant variable is similar to our last example, but with the added keyword const, which, of course, stands for constant. Adding the keyword const notifies the compiler of its unchanging nature and allows it to optimize storage space for that value (see Example 1.41).

# Example 1.41. Declaring constant variables.

```
```csharp
using System;

namespace Chapter1 {
    class Class1 {
        static void Main() {
            const int OurVariable = 1;
            Console.WriteLine("Our variable was assigned as "
                + OurVariable);
        }
    }
}
```
```

Adding the keyword const to a variable of data type float, double, or char would make them constants as well. Keep in mind that their values also have to be assigned as they are declared (see Example 1.42).
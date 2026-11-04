The main method is also easily adaptable to include both storage data types and the return statement (see Examples 2.38 and 2.39). Note that referencing a return statement from within the main method causes the immediate termination of that program.

# Example 2.38. Main function with data types.

```
using System;

namespace Chapter2 {
    class Class1 {
        static int Main() {
            return 0;
        }
    }
}
```

# Example 2.39. Empty return statements.

```
using System;

namespace Chapter2 {
    class Class1 {
        static void Main() {
            return;
        }
    }
}
```

# Passing Variables: Calls-By-Value

The call-by-value type mechanism is a mechanism used to transfer data between methods that does not allow for continued access to the original fields. The data is then considered to be a value type, which is appropriately stored on the "stack"—the computer's temporary memory—and will be removed, or "popped off," when that method is terminated. Again, the changes in these secondary variables will not affect the original fields, nor will there be deletions. The call-by-value formal parameters refer to the variables referenced from inside user-defined functions as demonstrated in Example 2.40 (a simple example that finds the square root of a number).
# LISTING 8.3: Accessing Properties before Initializing All Fields

```
// ERROR: The 'this' object cannot be used before
// all of its fields are assigned to
// public Angle(int hours, int minutes, int seconds)
// {
// Hours = hours; // Shorthand for this.Hours = hours;
// Minutes = minutes // Shorthand for this.Minutes = ...;
// Seconds = seconds // Shorthand for this.Seconds = ...;
// }
```

The error reports that methods and properties (Hours implies this.Hours) are accessed prior to the initialization of all fields. To resolve the issue, you need to initialize the fields directly, as demonstrated in Listing 8.1.

# ADVANCED TOPIC

# Using new with Value Types

Invoking the new operator on a reference type compiles to the CIL instruction newobj. new is available on value types as well, but in contrast, the underlying CIL instruction is initobj. This instruction initializes the memory with default values (the equivalent of assigning default(<type>) in C# 2.0).

Unlike classes, structs do not support finalizers. For local variable value types, memory is allocated on the stack, so there is no need for the garbage collector to handle the value type’s cleanup and no finalizer is called before the stack is unwound. For value types that are part of a reference type, the data is stored on the heap and memory is cleaned up as part of the reference object’s garbage collection.

# Language Contrast: C++—struct Defines Type with Public Members

In C++, the difference between structs and classes is simply that by default, a struct’s members are public. C# doesn’t include this subtle distinction. The contrast is far greater in C#, where struct significantly changes the memory behavior from that of a class.
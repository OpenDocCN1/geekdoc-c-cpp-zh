# # Types

C# is both a type-safe and statically typed language. These concepts go hand-in-hand and require you to inform the compiler of the data type for any variable you create. In return, the compiler guarantees that you can only store a compatible data type in that variable. This helps prevent common programming errors, leading to a more stable and secure application.

Types are divided into three main categories:

+   - Value types
- Reference types
- Type parameters

Put simply, a value type is completely self-contained and copied “by value.” This means that variables of a value type directly contain their data, and it is not possible for operations on one to affect the other. Value types are further categorized into structures, enumerated types, and nullable types.

A reference type contains a reference to the actual data, meaning it is possible for two variables to reference the same object, allowing the possibility that operations on one will affect the other. Reference types are further categorized into classes, arrays, interfaces, and delegates.
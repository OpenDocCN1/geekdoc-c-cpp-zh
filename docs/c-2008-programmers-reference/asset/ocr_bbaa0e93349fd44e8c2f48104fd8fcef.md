# ### Value Types versus Reference Types

For any discussion about value types and reference types, it is important to understand how the .NET Framework manages the data in memory.

Basically, the memory is divided into two parts — the stack and the heap. The stack is a data structure used to store value-type variables. When you create an `int` variable, the value is stored on the stack. In addition, any call you make to a function (method) is added to the top of the stack and removed when the function returns.

In contrast, the heap is used to store reference-type variables. When you create an instance of a class, the object is allocated on the heap and its address is returned and stored in a variable located on the stack.

Memory allocation and deallocation on the stack is much faster than on the heap, so if the size of the data to be stored is small, it's better to use a value-type variable than a reference-type variable. Conversely, if the size of data is large, it is better to use a reference-type variable.

C# supports two predefined reference types — `object` and `string` — which are described in the following table.

| C# Type | .NET Framework Type | Descriptions |
|---|---|---|
| `object` | `System.Object` | Root type from which all types in the CTS (Common Type System) derive |
| `string` | `System.String` | Unicode character string |

Chapter 4 explores the `System.Object` type, and Chapter 8 covers strings in more detail.

# # Enumerations

You can create your own set of named constants by using enumerations. In C#, you define an enumeration by using the `enum` keyword. For example, say that you need a variable to store the day of a week (Monday, Tuesday, Wednesday, and so on):

```
```csharp
    static void Main(string[] args)
    {
        int day = 1; //---1 to represent Monday---
        //...
        Console.ReadLine();
        return;
    }
```
```
![](bbox=[0.209, 0.134, 0.268, 0.171])

> Variables of reference types are called objects and are stored on the heap or managed heap, which is an area of memory that is reserved for storing a large amount of data. In addition, objects of reference types have variable lengths, that is, two objects of the same reference type can occupy different number of bytes in memory.

C# provides two predefined reference types, which are as follows:

+   - **The object type:** Represents the fundamental data type from which all other data types are created or derived. This data type is the base for both predefined and user-defined data types in C#.
+   - **The string type:** Represents a string or sequence of Unicode characters. Values of string data type are enclosed within a pair of double quotes (“ ”). You can perform various operations on strings, such as copying, comparing, and concatenating. Variables of the string data type are created by using the **string** keyword.

You can also create your own reference types in C#. The user-defined reference types can be classified as:

+   - **Classes:** Represent a data type that contains variables, methods, and properties. The variables, methods, properties, and other elements that a class contains are called members, and the instances of that class are called objects. Classes are created by using the **class** keyword.
+   - **Interfaces:** Represent a cohesive group containing only the declaration of programming elements, such as methods, events, and properties. You cannot create objects of an interface; however, you can implement it in several classes and use the containing elements. In C#, interfaces are created by using the **interface** keyword.
+   - **Arrays:** Represent an ordered collection of data or values that are of the same data type. The values in an array are stored at contiguous memory locations. This implies that the values are stored in sequential memory blocks.
+   - **Delegates:** Represent a data type that stores a reference or address of a particular method. A delegate behaves in the same way as the method to which it references. The declaration or signature of the delegate and the method to which it references must match. Delegates are created by using the **delegate** keyword.

# Pointer Types

A variable that holds the memory address of another variable is known as a pointer. Pointer types are used as the data type of variables declared as pointers. In C#, pointer types offer the same capabilities as offered by C and C++ languages. Pointers and references are similar as both represent memory address but the difference is that references are tracked by the garbage collector and pointers are not. C# uses delegates to maintain type safety and security in the context of references instead of using pointers. However, you can use pointers by defining an unsafe context (a simple code whose safety is not verified by the CLR). You can use the unsafe keyword to define an unsafe context. In other words, pointer types are used only in the unsafe context. Pointer types are not inherited from the Object class, which is the base class of all .NET types. You cannot convert pointer types to object type and vice-versa. A pointer variable is used to store the address of another variable. The following syntax shows the declaration of pointer type:

```
datatype* identifier;
```

After learning about data types in C#, let’s now learn about data type conversion.

# Explaining Data Type Conversion

Data type conversion refers to the process of converting the values of one data type into another data type. When the value of a variable of one data type is converted into value of another data type, only the data type of the value is changed; the value itself remains the same. In C#, the following types of conversions are available:

+   - Implicit conversion
+   - Explicit conversion

Let’s discuss both these conversion types, one by one.
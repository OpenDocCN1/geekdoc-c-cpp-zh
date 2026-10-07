# Language Contrast: C/C++—Pointer Declaration

In C/C++, multiple pointers within the same declaration are declared as follows:

int *p1, *p2;

Notice the * on p2; this makes p2 an int* rather than an int. In contrast, C# always places the * with the data type:

int* p1, p2;

The result is two variables of type int*. The syntax matches that of declaring multiple arrays in a single statement:

```
int[] array1, array2;
```

Pointers are an entirely new category of type. Unlike structs, enums, and classes, pointers don't ultimately derive from System.Object and are not even convertible to System.Object. Instead, they are convertible (explicitly) to System.IntPtr (which can be converted to System.Object).

In addition to custom structs that contain only unmanaged types, valid refer types include enums, predefined value types (byte, byte, short, ushort, int, uint, long, char, float, double, decimal, and bool), and pointer types (such as byte\*). Lastly, valid syntax includes void* pointers, which represent pointers to an unknown type.

# Assigning a Pointer

Once code defines a pointer, it needs to assign a value before accessing it. Just like reference types, pointers can hold the value null, which is their default value. The value stored by the pointer is the address of a location. Therefore, to assign the pointer, you must first retrieve the address of the data.

You could explicitly cast an int or a long into a pointer, but this rarely occurs without means of determining the address of a particular data value at execution time. Instead, you need to use the address operator (&) to retrieve the address of the value type:

```
byte* pData = &bytes[0]; // Compile error
```
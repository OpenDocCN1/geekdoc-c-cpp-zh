must be explicit. Implicit conversions are not available for such conversions. For example, it is perfectly legitimate to write the following:

```
int x = 10;
int* pX, pY;
pX = &x;
pY = pX;
*pY = 20;
uint y = (uint)pX;
int* pD = (int*)y;
```

The address held in the pointer pX is cast to a uint and stored in the variable y. You have then cast y back to an int* and stored it in the new variable pD. Hence, now pD also points to the value of x.

The primary reason for casting a pointer value to an integer type is to display it. The Console.Write() and Console.WriteLine() methods do not have any overloads that can take pointers, but will accept and display pointer values that have been cast to integer types:

```
Console.WriteLine("Address is " + pX);  // wrong -- will give a
                                         // compilation error
Console.WriteLine("Address is " + (uint)pX);  // OK
```

You can cast a pointer to any of the integer types. However, because an address occupies 4 bytes on 32-bit systems, casting a pointer to anything other than a uint, long, or ulong is almost certain to lead to overflow errors. (An int causes problems because its range is from roughly -2 billion to 2 billion, whereas an address runs from zero to about 4 billion.) When C# is released for 64-bit processors, an address will occupy 8 bytes. Hence, on such systems, casting a pointer to anything other than ulong is likely to lead to overflow errors. It is also important to be aware that the checked keyword does not apply to conversions involving pointers. For such conversions, exceptions will not be raised when overflows occur, even in a checked context. The .NET runtime assumes that if you are using pointers you know what you are doing, and are not worried about possible overflows.

# Casting Between Pointer Types

You can also explicitly convert between pointers pointing to different types. For example:

```
byte aByte = 8;
byte* pByte = &aByte;
double* pDouble = (double*)pByte;
```

# void Pointers

If you want to maintain a pointer, but do not want to specify what type of data it points to, you can declare it as a pointer to void:

```
int* pointerToInt;
void* pointerToVoid;
pointerToVoid = (void*)pointerToInt;
```
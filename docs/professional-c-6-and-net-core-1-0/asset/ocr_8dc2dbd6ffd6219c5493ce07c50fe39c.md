predefined types `uint`, `int`, `byte`, and so on, or to a struct). However, it is not possible to declare a pointer to a class or an array; this is because doing so could cause problems for the garbage collector. To work properly, the garbage collector needs to know exactly what class instances have been created on the heap, and where they are; but if your code started manipulating classes using pointers, you could very easily corrupt the information on the heap concerning classes that the .NET runtime maintains for the garbage collector. In this context, any data type that the garbage collector can access is known as a *managed type*. Pointers can only be declared as *unmanaged* types because the garbage collector cannot deal with them.

# Casting Pointers to Integer Types

Because a pointer really stores an integer that represents an address, you won’t be surprised to know that the address in any pointer can be converted to or from any integer type. Pointer-to-integer-type conversions must be explicit. Implicit conversions are not available for such conversions. For example, it is perfectly legitimate to write the following:

```
int x = 10;
int* pX, pY;
pX = &x;
pY = pX;
*pY = 20;
ulong y = (ulong)pX;
int* pD = (int*)y;
```

The address held in the pointer `pX` is cast to a `uint` and stored in the variable `y`. You have then cast `y` back to an `int*` and stored it in the new variable `pD`. Hence, now `pD` also points to the value of `x`.

The primary reason for casting a pointer value to an integer type is to display it. The interpolation string (and similarly `Console.Write`) does not have any overloads that can take pointers, but they do accept and display pointer values that have been cast to integer types:

```
WriteLine($"Address is {pX}"); // wrong -- will give a
compilation error
WriteLine($"Address is {(ulong)pX}"); // OK
```

You can cast a pointer to any of the integer types. However, because an address occupies 4 bytes on 32-bit systems, casting a pointer to anything other than a `uint`, `long`, or `ulong` is almost certain to lead to overflow errors. (An `int` causes problems because its range is from roughly −2 billion to 2 billion, whereas an address runs from zero to about 4 billion.) If you are creating a 64-bit application, you need to cast the pointer to `ulong`.

It is also important to be aware that the `checked` keyword does not apply to conversions involving pointers. For such conversions, exceptions are not raised when overflows occur, even in a `checked` context. The .NET runtime assumes that if you are using pointers, you know what you are
There are two ways to implement Dispose method,

+   1. Implement Dispose using 'SafeHandle' Class (It is inbuilt abstract class which has 'CriticalFinalizerObject' and 'IDisposable' interface has been implemented)
+   2. Object.Finalize method to be override (This method is clean unmanaged resources used by particular object before it is destroyed)

# 13.1.2 Pointers in C#

# 13.1.2.1 Pointers

C# supports pointers in a limited extent. Pointers are defined as a variable that contains the memory address of another variable.

Pointers can be declared as,

```
type *var_name;
int* iptr;
```

Here * is called a de-reference operator and iptr is the variable that contains the address of integer type variable.

```
int num =30;
int *iptr = & num;  // where &num is the memory address of num variable
Console.WriteLine((int)iptr);  // displaying memory address stored in iptr
//below code line outputs- 30 (displaying value at memory address held by iptr)
Console.WriteLine(*iptr);
```

# 13.1.2.2 Unsafe Code

+   - The C# statements can be executed either as in a safe or in an unsafe context. In C# any code involving pointers requires an unsafe context. Unlike reference types, pointer types are not tracked by the default garbage collection mechanism. That is the statements marked as unsafe by using the keyword unsafe runs outside the control of Garbage Collector. For the same reason pointers are not allowed to point to a reference type or even to a structure type which contains a reference type. Pointers can point to only unmanaged types which include all basic data types, enum types, other pointer types and structs which contain only unmanaged types.
+   - There are two more concepts in C# that one must be aware of before discussing pointers and these are Managed Code and Unmanaged Code.
+   
+   Managed Code : Managed code runs under the control of CLR. Managed code is trackable and can be garbage collected. Managed code runs by CLR under managed environment and have access to all CLR features, CLR verifies the security and type safety of managed code.
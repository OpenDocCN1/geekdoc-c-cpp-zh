
There are two ways to implement the `Dispose` method:

1. Implement `Dispose` using the `SafeHandle` class (it is an inbuilt abstract class which has `CriticalFinalizerObject` and the `IDisposable` interface has been implemented).
2. `Object.Finalize` method to be overridden (this method cleans unmanaged resources used by a particular object before it is destroyed).

## 13.1.2 Pointers in C#

### 13.1.2.1 Pointers

C# supports pointers to a limited extent. Pointers are defined as a variable that contains the memory address of another variable.

Pointers can be declared as:

```csharp
type *var_name;
int* iptr;
```

Here `*` is called a dereference operator and `iptr` is the variable that contains the address of an integer type variable.

```csharp
int num = 30;
int* iptr = &num;  // where &num is the memory address of num variable
Console.WriteLine((int)iptr);  // displaying memory address stored in iptr
// below code line outputs - 30 (displaying value at memory address held by iptr)
Console.WriteLine(*iptr);
```

### 13.1.2.2 Unsafe Code

- The C# statements can be executed either in a safe or in an unsafe context. In C#, any code involving pointers requires an unsafe context. Unlike reference types, pointer types are not tracked by the default garbage collection mechanism. That is, the statements marked as unsafe by using the keyword `unsafe` run outside the control of the garbage collector. For the same reason, pointers are not allowed to point to a reference type or even to a structure type which contains a reference type. Pointers can point only to unmanaged types, which include all basic data types, enum types, other pointer types, and structs which contain only unmanaged types.

- There are two more concepts in C# that one must be aware of before discussing pointers, and these are Managed Code and Unmanaged Code.

  **Managed Code:** Managed code runs under the control of CLR. Managed code is trackable and can be garbage collected. Managed code runs by CLR under a managed environment and has access to all CLR features; CLR verifies the security and type safety of managed code.

  **Unmanaged Code:** Unmanaged code cannot be executed by CLR; it is executed directly by the computer CPU and has no access to CLR features. As CLR has no authority on unmanaged code, CLR cannot verify the security and type safety of unmanaged code.

### 13.1.2.3 Types of Pointers

In an unsafe context, a variable type can be a reference type, value type, or pointer type, but pointers can only point to:

- primitive value types
- struct containing value types only
- other pointer types

In C#, pointers cannot point to reference types because reference types are managed by CLR and can be garbage collected, but on the other hand pointers run under an unmanaged environment and cannot be tracked by GC (garbage collector). A reference can be garbage collected any time when a pointer pointing to it is dereferenced. So in C#, pointers cannot point to:

- reference types
- struct containing reference types

### 13.1.2.4 Pinning an Object

The C# garbage collector can move the objects in memory as it wishes during the garbage collection process. C# provides a special keyword `fixed` to tell the garbage collector not to move an object. That means this fixes the in-memory locations of the value types pointed to. This is what is known as pinning in C#. The `fixed` statement is typically implemented by generating tables that describe to the garbage collector, so as to indicate which objects are to remain fixed in which regions of executable code. Thus, as long as a garbage collector process doesn't actually occur during execution of `fixed` statements, there is very little cost associated with this. However, when a garbage collector process does occur, fixed objects may cause fragmentation of the heap. Hence, objects should be fixed only when absolutely necessary and only for the shortest amount of time.

### 13.1.2.5 Working of Pointers in C#

**Example**

```csharp
// Pointers in C# -
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace Pointers
{
    class Demo
    {
        public void Method()
        {
            unsafe
            {
                int a = 40;
                int b = 20;
                int* ptr1 = &a;
                int* ptr2 = &b;
                Console.WriteLine(*ptr1);   // displaying the value
                Console.WriteLine(*ptr2);   // displaying the value
                Console.WriteLine((int)ptr1); // displaying the address
                Console.WriteLine((int)ptr2); // displaying the address
            }
        }
    }
    class DemoExample
    {
        // main method
        public static void Main()
        {
            Demo d = new Demo();
            d.Method();
        }
    }
}
```

There are different ways to execute statements as unsafe, like a modifier, constructor, etc. In the above example, a group of statements are marked as unsafe. In the above code, there are two variables `a` and `b` with values 40 and 20 respectively, and pointers contain their addresses. `Console.WriteLine()` is used to display the values and addresses of the variables.

### 13.1.2.6 Pointers and Conversions

In C#, pointer types do not inherit from `object` and no conversion exists between pointer types and objects. That means boxing and unboxing are not supported by pointers. But C# supports conversions between different pointer types, and between pointer types and integral types. C# supports both implicit and explicit pointer conversions within an unsafe context. The implicit conversions are:

1. From any pointer type to `void*` type.
2. From null type to any pointer type.

The cast operator `()` is necessary for any explicit type conversions. The explicit type conversions are:

1. From any pointer type to any other pointer type.
2. From `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong` to any pointer type.
3. From any pointer type to `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong` types.

### 13.1.2.7 Pointer Arithmetic

In an unsafe context, the `++` and `--` operators can be applied to pointer variables of all types except `void*` type. Pointer arithmetic works on the size of the data type whose address they are holding and the actual address held. In pointer arithmetic, it would be absurd to work on values. Thus, for every pointer type `P*`, the following operators are implicitly overloaded:

```csharp
P* operator ++(P* x);
P* operator --(P* x);
```

The `++` operator adds `sizeof(P)` to the address contained in the variable, and the `--` operator subtracts `sizeof(P)` from the address contained in the variable for a pointer variable of type `P*`.

In an unsafe context, a constant can be added to or subtracted from a pointer variable. Similarly, a pointer variable can be subtracted from another pointer variable. But it is not allowed to add two pointer variables in C#.

In an unsafe context, relational operators like `==`, `!=`, `<=`, `>=`, `<`, and `>` can be applied to values of all pointer types. The multiplication and division of a pointer variable with a constant or with another pointer variable is not possible in C#.

### 13.1.2.8 Stack Allocation

In an unsafe context, a local declaration may include a stack allocation initializer, which allocates memory from the call stack. In C#, the operator `stackalloc P[Exp]` requires `P` to be an unmanaged type and `Exp` to be an expression of type `int`. The above construct allocates `Exp * sizeof(P)` bytes from the call stack and produces a pointer of the type `P*` to the newly allocated block. If `Exp` is negative, a `System.OverflowException` is thrown. If there is not enough memory to allocate, a `System.StackOverflowException` is thrown. The content of newly allocated memory is undefined. There is no way to implicitly free memory allocated using `stackalloc`. Instead, all stack-allocated memory blocks are automatically discarded once the function returns.

### 13.1.2.9 Pointers and Arrays

In C#, array elements can be accessed by using pointer notations as shown in the below program.

```csharp
using System;

class DemoClass
{
    public unsafe void Method()
    {
        int[] iArray = new int[10];
        for (int cnt = 0; cnt < 10; cnt++)
        {
            iArray[cnt] = cnt * cnt;
        }
        fixed (int* ptr = iArray)
            Display(ptr);
        // Console.WriteLine(*(ptr + 2));
        // Console.WriteLine((int)ptr);
    }

    public unsafe void Display(int* pt)
    {
        for (int itr = 0; itr < 10; itr++)
        {
            Console.WriteLine(*(pt + itr));
        }
    }
}

class UseDemo
{
    public static void Main()
    {
        DemoClass dc = new DemoClass();
        dc.Method();
    }
}
```

### 13.1.2.10 Pointers and Structures

The structures in C# are value types. Pointers can be used with structures if they contain only value types as their members. This is illustrated in the below program.

```csharp
using System;

struct DemoStruct
{
    public int n1;
    public int n2;
}
```

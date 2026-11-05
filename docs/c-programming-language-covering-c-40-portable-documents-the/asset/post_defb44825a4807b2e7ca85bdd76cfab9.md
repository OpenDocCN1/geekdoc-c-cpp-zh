
```
fixed-size-buffer-modifier:
  new
  public
  protected
  internal
  private
  unsafe
```

```
buffer-element-type:
  type
```

```
fixed-size-buffer-declarators:
  fixed-size-buffer-declarator
  fixed-size-buffer-declarator , fixed-size-buffer-declarators
```

```
fixed-size-buffer-declarator:
  identifier [ constant-expression ]
```

A fixed-size buffer declaration may include a set of attributes (§17), a new modifier (§10.2.2), a valid combination of the four access modifiers (§10.2.3), and an unsafe modifier (§18.1). The attributes and modifiers apply to all of the members declared by the fixed-size buffer declaration. It is an error for the same modifier to appear multiple times in a fixed-size buffer declaration.

A fixed-size buffer declaration is not permitted to include the static modifier.

The buffer element type of a fixed-size buffer declaration specifies the element type of the buffer(s) introduced by the declaration. The buffer element type must be one of the pre-defined types sbyte, byte, short, ushort, int, uint, long, ulong, char, float, double, or bool.

The buffer element type is followed by a list of fixed-size buffer declarators, each of which introduces a new member. A fixed-size buffer declarator consists of an identifier that names the member, followed by a constant expression enclosed in "[" and "]" tokens. The constant expression denotes the number of elements in the member introduced by that fixed-size buffer declarator. The type of the constant expression must be implicitly convertible to type int, and the value must be a non-zero positive integer.

The elements of a fixed-size buffer are guaranteed to be laid out sequentially in memory.

A fixed-size buffer declaration that declares multiple fixed-size buffers is equivalent to multiple declarations of a single fixed-size buffer with the same attributes and element types. For example,

```
unsafe struct A
{
    public fixed int x[5], y[10], z[100];
}
```

is equivalent to

```
unsafe struct A
{
    public fixed int x[5];
    public fixed int y[10];
    public fixed int z[100];
}
```

## 18.7.2 Fixed-Size Buffers in Expressions

Member lookup (§7.3) of a fixed-size buffer member proceeds exactly like member lookup of a field.

A fixed-size buffer can be referenced in an expression using a simple-name (§7.5.2) or a member-access (§7.5.4).

When a fixed-size buffer member is referenced as a simple name, the effect is the same as a member access of the form this.I, where I is the fixed-size buffer member.

In a member access of the form E.I, if E is of a struct type and a member lookup of I in that struct type identifies a fixed-size member, then E.I is evaluated and classified as follows:

- If the expression E.I does not occur in an unsafe context, a compile-time error occurs.
- If E is classified as a value, a compile-time error occurs.
- Otherwise, if E is a moveable variable (§18.3) and the expression E.I is not a fixed-pointer-initializer (§18.6), a compile-time error occurs.
- Otherwise, E references a fixed variable and the result of the expression is a pointer to the first element of the fixed-size buffer member I in E. The result is of type S*, where S is the element type of I, and is classified as a value.

The subsequent elements of the fixed-size buffer can be accessed using pointer operations from the first element. Unlike access to arrays, access to the elements of a fixed-size buffer is an unsafe operation and is not range checked.

The following example declares and uses a struct with a fixed-size buffer member:

```
unsafe struct Font
{
    public int size;
    public fixed char name[32];
}
```

```
class Test
{
    unsafe static void PutString(string s, char* buffer, int bufSize)
    {
        int len = s.Length;
        if (len > bufSize) len = bufSize;
        for (int i = 0; i < len; i++) buffer[i] = s[i];
        for (int i = len; i < bufSize; i++) buffer[i] = (char)0;
    }
    unsafe static void Main()
    {
        Font f;
        f.size = 10;
        PutString("Times New Roman", f.name, 32);
    }
}
```

## 18.7.3 Definite Assignment Checking

Fixed-size buffers are not subject to definite assignment checking (§5.3), and fixed-size buffer members are ignored for purposes of definite assignment checking of struct type variables.

When the outermost containing struct variable of a fixed-size buffer member is a static variable, an instance variable of a class instance, or an array element, the elements of the fixed-size buffer are automatically initialized to their default values (§5.2). In all other cases, the initial content of a fixed-size buffer is undefined.

## 18.8 Stack Allocation

In an unsafe context, a local variable declaration (§8.5.1) may include a stack allocation initializer that allocates memory from the call stack.

> ERIC LIPPERT  This is a bit overspecific; there is no requirement that a particular CPU allow allocation of arbitrary memory on its call stack. For example, the CLR could be implemented on a CPU architecture that keeps two stacks—one for storage of local variables and one for tracking return addresses. (Such architectures prevent the stack-rewriting attacks that plagued the x86 architecture.) Really, what we ought to say here is simply that an immobile local memory store is associated with each method invocation, and that stackalloc allocates memory out of that store. In a typical implementation, that store will be the call stack, but that's an implementation detail.

local-variable-initializer:
...
stackalloc-initializer

stackalloc-initializer:
stackalloc unmanaged-type [ expression ]

The unmanaged-type indicates the type of the items that will be stored in the newly allocated location, and the expression indicates the number of these items. Taken together, these specify the required allocation size. Since the size of a stack allocation cannot be negative, it is a compile-time error to specify the number of items as a constant expression that evaluates to a negative value.

A stack allocation initializer of the form stackalloc T[E] requires T to be an unmanaged type (§18.2) and E to be an expression of type int. The construct allocates E * sizeof(T) bytes from the call stack and returns a pointer, of type T*, to the newly allocated memory. If E is a negative value, then the behavior is undefined. If E is zero, then no allocation is made, and the pointer returned is implementation-defined. If there is not enough memory available to allocate a block of the given size, a System.StackOverflowException is thrown.

The content of the newly allocated memory is undefined.

Stack allocation initializers are not permitted in catch or finally blocks (§8.10).

There is no way to explicitly free memory allocated using stackalloc. All stack allocated memory blocks created during the execution of a function member are automatically discarded when that function member returns. This corresponds to the alloca function, an extension commonly found in C and C++ implementations.

In the example

```
using System;
class Test
{
    static string IntToString(int value)
    {
        int n = value >= 0 ? value : -value;
        unsafe
        {
            char* buffer = stackalloc char[16];
            char* p = buffer + 16;
            do
            {
                *--p = (char)(n % 10 + '0');
                n /= 10;
            } while (n != 0);
        }
        if (value < 0) *--p = '-';
        return new string(p, 0, (int)(buffer + 16 - p));
    }
    static void Main()
    {
        Console.WriteLine(IntToString(12345));
        Console.WriteLine(IntToString(-999));
    }
}
```

a stackalloc initializer is used in the IntToString method to allocate a buffer of 16 characters on the stack. The buffer is automatically discarded when the method returns.

## 18.9 Dynamic Memory Allocation

Except for the stackalloc operator, C# provides no predefined constructs for managing non-garbage-collected memory. Such services are typically provided by supporting class libraries or imported directly from the underlying operating system. For example, the Memory class below illustrates how the heap functions of an underlying operating system might be accessed from C#:

```
using System;
using System.Runtime.InteropServices;

public unsafe class Memory
{
    // Handle for the process heap. This handle is used
    // in all calls to the
    // HeapXXX APIs in the methods below.
    static int ph = GetProcessHeap();
    // Private instance constructor to prevent instantiation.
    private Memory() { }
    // Allocates a memory block of the given size.
    // The allocated memory is
    // automatically initialized to zero.
    public static void* Alloc(int size)
    {
        void* result = HeapAlloc(ph, HEAP_ZERO_MEMORY, size);
        if (result == null) throw new OutOfMemoryException();
        return result;
    }
    // Copies count bytes from src to dst. The source and destination
    // blocks are permitted to overlap.
```

```
```csharp
unsafe struct A
{
    public fixed int x[5];
    public fixed int y[10];
    public fixed int z[100];
}
```
```

*end example]*

# 23.8.3 Fixed-size buffers in expressions

Member lookup (§12.5) of a fixed-size buffer member proceeds exactly like member lookup of a field.

A fixed-size buffer can be referenced in an expression using a *simple-name* (§12.6.3) or a *member-access* (§12.6.5).

When a fixed-size buffer member is referenced as a simple name, the effect is the same as a member access of the form this.I, where I is the fixed-size buffer member.

In a member access of the form E.I, if E is of a struct type and a member lookup of I in that struct type identifies a fixed-size member, then E.I is evaluated and classified as follows:

+   - If the expression E.I does not occur in an unsafe context, a compile-time error occurs.
+   - If E is classified as a value, a compile-time error occurs.
+   - Otherwise, if E is a movable variable (§23.4) and the expression E.I is not a fixed-pointer-initializer (§23.7), a compile-time error occurs.
+   - Otherwise, E references a fixed variable and the result of the expression is a pointer to the first element of the fixed-size buffer member I in E. The result is of type S*, where S is the element type of I, and is classified as a value.

The subsequent elements of the fixed-size buffer can be accessed using pointer operations from the first element. Unlike access to arrays, access to the elements of a fixed-size buffer is an unsafe operation and is not range checked.

*[Example: The following declares and uses a struct with a fixed-size buffer member.*

```
```csharp
unsafe struct Font
{
    public int size;
    public fixed char name[32];
}

class Test
{
    unsafe static void PutString(string s, char* buffer, int bufSize) {
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
```

*end example]*

# 23.8.4 Definite assignment checking

Fixed-size buffers are not subject to definite assignment-checking (§10.4), and fixed-size buffer members are ignored for purposes of definite-assignment checking of struct type variables.
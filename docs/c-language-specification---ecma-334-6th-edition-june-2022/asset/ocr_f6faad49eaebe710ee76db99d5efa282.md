A fixed-size buffer can be referenced in an expression using a simple_name (§11.6.3) or a member_access (§11.6.5).

When a fixed-size buffer member is referenced as a simple name, the effect is the same as a member access of the form this.I, where I is the fixed-size buffer member.

In a member access of the form E.I, if E is of a struct type and a member lookup of I in that struct type identifies a fixed-size member, then E.I is evaluated and classified as follows:

+   - If the expression E.I does not occur in an unsafe context, a compile-time error occurs.
+   - If E is classified as a value, a compile-time error occurs.
+   - Otherwise, if E is a moveable variable (§22.4) and the expression E.I is not a fixed_pointer_initializer (§22.7), a compile-time error occurs.
+   - Otherwise, E references a fixed variable and the result of the expression is a pointer to the first element of the fixed-size buffer member I in E. The result is of type S*, where S is the element type of I, and is classified as a value.

The subsequent elements of the fixed-size buffer can be accessed using pointer operations from the first element. Unlike access to arrays, access to the elements of a fixed-size buffer is an unsafe operation and is not range checked.

Example: The following declares and uses a struct with a fixed-size buffer member.

```
unsafe struct Font
{
    public int size;
    public fixed char name[32];
}

class Test
{
    unsafe static void PutString(string s, char* buffer, int bufSize)
    {
        int len = s.Length;
        if (len > bufSize)
        {
            len = bufSize;
        }
        for (int i = 0; i < len; i++)
        {
            buffer[i] = s[i];
        }
        for (int i = len; i < bufSize; i++)
        {
            buffer[i] = (char)0;
        }
    }

    unsafe static void Main()
    {
        Font f;
        f.size = 10;
        PutString("Times New Roman", f.name, 32);
    }
}
```
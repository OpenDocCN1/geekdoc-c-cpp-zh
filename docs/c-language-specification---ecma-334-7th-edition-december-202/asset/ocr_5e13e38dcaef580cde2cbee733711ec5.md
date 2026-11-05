```
long* p6 = stackalloc[] { 11, 12L, 13 };
// Converts all and returns long*
long* p7 = stackalloc long[] { 11, 12, 13 };
}
```

*end example*

Unlike access to arrays or stackalloc'ed blocks of Span<T> type, access to the elements of a stackalloc'ed block of pointer type is an unsafe operation and is not range checked.

Example: In the following code

```
class Test
{
    static string IntToString(int value)
    {
        if (value == int.MinValue)
        {
            return "-2147483648";
        }
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
            if (value < 0)
            {
                *--p = '-';
            }
            return new string(p, 0, (int)(buffer + 16 - p));
        }
    }
    static void Main()
    {
        Console.WriteLine(IntToString(12345));
        Console.WriteLine(IntToString(-999));
    }
}
```

a stackalloc expression is used in the IntToString method to allocate a buffer of 16 characters on the stack. The buffer is automatically discarded when the method returns.

Note, however, that IntToString can be rewritten in safe mode; that is, without using pointers, as follows:

```
class Test
{
    static string IntToString(int value)
    {
        if (value == int.MinValue)
        {

```
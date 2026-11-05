```
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

static void Main()
{
    Console.WriteLine(IntToString(12345));
    Console.WriteLine(IntToString(-999));
}
```

a stackalloc initializer is used in the IntToString method to allocate a buffer of 16 characters on the stack. The buffer is automatically discarded when the method returns.

end example

Except for the stackalloc operator, C# provides no predefined constructs for managing non-garbage collected memory. Such services are typically provided by supporting class libraries or imported directly from the underlying operating system.

**End of conditionally normative text.**
# Using StructLayoutAttribute for Sequential Layout

Some APIs invoke types that have no corresponding name. Calling these types requires declaration of the type in managed code. You declare the unmanaged COLORREF struct, for example, in managed code (see Listing 23.5).

Listing 23.5: Declaring Types from Unmanaged Structs

```
[StructLayout(LayoutKind.Sequential)]
struct ColorRef
{
    public byte Red;
    public byte Green;
    public byte Blue;
    // Turn off the warning about not accessing Unused
    gma warning disable 414
    private byte Unused;
    gma warning restore 414

    public ColorRef(byte red, byte green, byte blue)
    {
        Blue = blue;
        Green = green;
        Red = red;
        Unused = 0;
    }
}
```

Various Microsoft Windows APIs use COLORREF to represent RGB colors (i.e., levels of red, green, and blue).

The key in the Listing 23.5 declaration is StructLayoutAttribute. By default, managed code can optimize the memory layouts of types, so layouts may not be sequential from one field to the next. For sequential layouts so that a type maps directly and can be copied for bit (blitted) from managed to unmanaged code, and vice versa, you add the StructLayoutAttribute with the LayoutKind.Sequential enum value. This is also useful when writing data to and from filestreams a sequential layout may be expected.

Since the unmanaged (C++) definition for struct does not map to the C# definition, there is no direct mapping of unmanaged struct to managed struct. Instead, developers should follow the usual C# guidelines about whether the type should
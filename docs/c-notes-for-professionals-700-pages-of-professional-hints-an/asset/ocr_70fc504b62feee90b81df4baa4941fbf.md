# Chapter 160: Including Font Resources

| Parameter | Details |
|-----------|---------|
| fontbytes | byte array from the binary .ttf |

# Section 160.1: Instantiate 'Fontfamily' from Resources

```
public FontFamily Maneteke = GetResourceFontFamily(Properties.Resources.manteka);
```

![](bbox=[0.04, 0.23, 0.95, 0.45])

# Section 160.2: Integration method

```
```csharp
public static FontFamily GetResourceFontFamily(byte[] fontbytes)
{
    PrivateFontCollection pfc = new PrivateFontCollection();
    IntPtr fontMemPointer = Marshal.AllocCoTaskMem(fontbytes.Length);
    Marshal.Copy(fontbytes, 0, fontMemPointer, fontbytes.Length);
    pfc.AddMemoryFont(fontMemPointer, fontbytes.Length);
    Marshal.FreeCoTaskMem(fontMemPointer);
    return pfc.Families[0];
}
```
```

# Section 160.3: Usage with a 'Button'

```
```csharp
public static class Res
{
    /// <summary>
    /// URL: https://www.behance.net/gallery/2846011/Manteka
    /// </summary>
    public static FontFamily Maneteke = GetResourceFontFamily(Properties.Resources.manteka);

    public static FontFamily GetResourceFontFamily(byte[] fontbytes)
    {
        PrivateFontCollection pfc = new PrivateFontCollection();
        IntPtr fontMemPointer = Marshal.AllocCoTaskMem(fontbytes.Length);
        Marshal.Copy(fontbytes, 0, fontMemPointer, fontbytes.Length);
        pfc.AddMemoryFont(fontMemPointer, fontbytes.Length);
        Marshal.FreeCoTaskMem(fontMemPointer);
        return pfc.Families[0];
    }
}
```
```
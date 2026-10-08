# **LISTING 5.3 A Flags Enumeration**

```
[Flags]
public enum Days
{
    None = 0,
    Sunday = 0x001,
    Monday = 0x002,
    Tuesday = 0x004,
    Wednesday = 0x008,
    Thursday = 0x010,
    Friday = 0x020,
    Saturday = 0x040,
}
```

To allow the values of a flags enumeration to be combined, all the values must be powers of two. This is necessary because when multiple values are combined, there must still be a way to identify which discrete values make up that combination. As a result, when defining a flags enumeration, you must always specify the values.

![](bbox=[0.06, 0.42, 0.18, 0.465])

# **The Flags Attribute**

Another difference between a regular enum and a flags enum is the use of the Flags attribute, which specifies additional metadata about the enumeration. The Flags attribute also changes the string representation of the enumeration value (from the ToString method) when used with a value made by combining other values.

Although you are not required to use the Flags attribute, it is strongly recommended because it provides a clear indication of intent, not just to the compiler but also to other programmers.

Unlike simple enumerations in which the zero value can be either None or the most common default, flags enumerations should always name the zero value None, and it should always mean that all flags are not set.

# ▼ **Try It Yourself**

# **Working with Flags Enumerations**

By following these steps, you modify the Days enumeration to be a flags enumeration and add some of the commonly used combinations. If you closed Visual Studio, repeat the previous exercise first.

+   1. Modify the Days enumeration to the one shown in Listing 5.3.
2. Add the following combinations:
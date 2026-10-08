insertion will begin. To remove data, you use the Remove method and indicate the starting position where the removal begins and the number of characters to remove.

The Replace method, or one of its overloads, can be used to replace characters within the current StringBuilder string with another specified character. The Replace method also supports replacing characters within a substring of the current StringBuilder string, specified by a starting position and length.

![](bbox=[0.06, 0.26, 0.18, 0.3])

**StringBuilder Capacity**

Internally, the *StringBuilder* string is maintained in a buffer to accommodate concatenation. The *StringBuilder* needs to allocate additional memory only if the buffer does not have enough room to accommodate the new data.

The default size, or capacity, for this internal buffer is 16 characters. When the buffer reaches capacity, additional buffer space is allocated for an additional amount of characters as specified by the *capacity*. *StringBuilder* also has a maximum capacity, which is *Int32.MaxValue*, or $2^{33}$, characters.

The length of the current string can be set using the *Length* property. By setting the *length* to a value that is larger than the current capacity, the capacity is automatically changed. Similarly, by setting the *Length* to a value that is less than the current capacity, the current string is shortened.

# ## Type Formatting

Formatting allows you to convert an instance of a class, structure, or enumeration value to a string representation. Every type that derives from *System.Object* automatically inherits a parameterless *ToString* method, which, by default, returns the name of the type. All the predefined value types have overridden *ToString* to return a general format for the type.

Because getting the name of the type from *ToString* isn't generally useful, you can override the *ToString* method and provide a meaningful string representation of your type. Listing 8.8 shows the *Contact* class overriding the *ToString* method.

+   LISTING 8.8 Overriding ToString

```
class Contact
{
    private string firstName;
    private string lastName;

    public override string ToString()
    {
        return firstName + " " + lastName;
    }
}
```
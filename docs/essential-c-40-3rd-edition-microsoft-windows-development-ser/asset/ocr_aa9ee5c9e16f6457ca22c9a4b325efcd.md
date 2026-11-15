```
file.Attributes);
FileAttributes attributes =
    (FileAttributes)Enum.Parse(typeof(FileAttributes),
    file.Attributes.ToString());
Console.WriteLine(attributes);
// ...
}
}
```

Output 17.6 shows the results of Listing 17.21.

# Output 17.6:

```
"ReadOnly | Hidden" outputs as "ReadOnly, Hidden"
```

The flag documents that the enumeration values can be combined. Furthermore, it changes the behavior of the ToString() and Parse() methods. For example, calling ToString() on an enumeration that is decorated with FlagsAttribute writes out the strings for each enumeration flag that is set. In Listing 17.21, FileAttributes.ToString() returns "ReadOnly, Hidden" rather than the 3 it would have returned without the FlagsAttribute flag. If two enumeration values are the same, the ToString() call would return the first one. As mentioned earlier, however, you should use this with caution because it is not localizable.

Parsing a value from a string to the enumeration also works, provided each enumeration value identifier is separated by a comma.

It is important to note that FlagsAttribute does not automatically assign the unique flag values or check that they have unique values. The values of each enumeration item still must be assigned explicitly.

# Predefined Attributes

The AttributeUsageAttribute attribute has a special characteristic that you didn't see in the custom attributes you have created thus far in this book. This attribute affects the behavior of the compiler, causing the compiler to sometimes report an error. Unlike the reflection code you wrote
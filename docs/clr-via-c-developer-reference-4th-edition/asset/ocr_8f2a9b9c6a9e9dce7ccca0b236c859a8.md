+   4. Each string is looked up in the enum type's defined symbols. If the symbol is not found, Parse throws a System.Argument and TryParse returns false. If the symbol is found, bitwise-OR its numeric value into a running result, and then look up the next token.

+   5. If all tokens have been sought and found, return the result.

You should never use the IsDefined method with flag-enumerated types. It won't work for two reasons:

+   - If you pass a string to IsDefined, it doesn't split the string into separate tokens to look up; it will attempt to look up the string as though it were one big symbol with commas in. Because you can't define an enum with a symbol that has commas in, it will never be found.

+   - If you pass a numeric value to IsDefined, it checks whether the enumerated type defines a single symbol whose numeric value matches the passed-in-number. Because this is unlikely to be bit flags, IsDefined will usually return false.

# # Adding Methods to Enumerated Types

Earlier in this chapter, I mentioned that you cannot define a method as part of an enumerated type. And, for many years, this has saddened me because there are many occasions when I would love to have been able to supply some methods to my enumerated type. Fortunately, I can use C# extension method feature (discussed in Chapter 8, "Methods") to simulate adding methods to an enumerated type.

If I want to add some methods to the FileAttributes type, I can define a static class with extension methods as follows.

```
internal static class FileAttributesExtensionMethods {
    public static bool IsSet(FileAttributes flags, FileAttributes flagTest) {
        if (flagTest == 0)
            throw new ArgumentOutOfRangeException("flagTest", "Value must not be 0");
        return (flags & flagTest);
    }
}
```

```
public static bool IsClear(FileAttributes flags, FileAttributes flagTest) {
        if (flagTest == 0)
            throw new ArgumentOutOfRangeException("flagTest", "Value must not be 0");
        return !IsSet(flags, flagTest);
    }
```

```
public static bool AnyFlagsSet(FileAttributes flags, FileAttributes testFlags) {
        return (flags & testFlags) != 0;
    }
```

```
public static FileAttributes Set(FileAttributes flags, FileAttributes setFlags) {
        return flags | setFlags;
    }
```
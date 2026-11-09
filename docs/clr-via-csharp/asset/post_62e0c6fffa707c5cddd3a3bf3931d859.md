
Because **Actions** is an enumerated type, you can use all of the methods described in the previous section when working with bit-flag enumerated types. However, it would be nice if some of those functions behaved a little differently. For example, let's say you had the following code:

```csharp
Actions actions = Actions.Read | Actions.Delete;  // 0x0005
Console.WriteLine(actions.ToString());              // "Read, Delete"
```

When **ToString** is called, it attempts to translate the numeric value into its symbolic equivalent. The numeric value is 0x0005, which has no symbolic equivalent. However, the **ToString** method detects the existence of the **[Flags]** attribute on the **Actions** type, and **ToString** now treats the numeric value not as a single value but as a set of bit flags. Because the 0x0001 and 0x0004 bits are set, **ToString** generates the following string: "Read, Delete." If you remove the **[Flags]** attribute from the **Actions** type, **ToString** would return "5."

I discussed the **ToString** method in the previous section, and I showed that it offered three ways to format the output: "G" (general), "D" (decimal), and "X" (hex). When you're formatting an instance of an enumerated type by using the general format, the type is first checked to see if the **[Flags]** attribute is applied to it. If this attribute is not applied, a symbol matching the numeric value is looked up and returned. If the **[Flags]** attribute is applied, **ToString** works like this:

- 1. The set of numeric values defined by the enumerated type is obtained, and the numbers are sorted in descending order.
- 2. Each numeric value is bitwise-ANDed with the value in the enum instance, and if the result equals the numeric value, the string associated with the numeric value is appended to the output string, and the bits are considered accounted for and are turned off. This step is repeated until all numeric values have been checked or until the enum instance has all of its bits turned off.
- 3. If, after all the numeric values have been checked, the enum instance is still not 0, the enum instance has some bits turned on that do not correspond to any defined symbols. In this case, **ToString** returns the original number in the enum instance as a string.
- 4. If the enum instance's original value wasn't 0, the string with the comma-separated set of symbols is returned.
- 5. If the enum instance's original value was 0 and if the enumerated type has a symbol defined with a corresponding value of 0, the symbol is returned.
- 6. If we reach this step, "0" is returned.

If you prefer, you could define the **Actions** type without the **[Flags]** attribute and still get the correct string by using the "F" format:

```csharp
// [Flags]    // Commented out now
internal enum Actions {
    None    = 0,
    Read    = 0x0001,
    Write   = 0x0002,
    ReadWrite = Actions.Read | Actions.Write,
    Delete  = 0x0004,
    Query   = 0x0008,
    Sync    = 0x0010
}
```

```csharp
Actions actions = Actions.Read | Actions.Delete; // 0x0005
Console.WriteLine(actions.ToString("F"));       // "Read, Delete"
```

If the numeric value has a bit that cannot be mapped to a symbol, the returned string will contain just a decimal number indicating the original numeric value; no symbols will appear in the string.

Note that the symbols you define in your enumerated type don't have to be pure powers of 2. For example, the **Actions** type could define a symbol called **All** with a value of 0x001F. If an instance of the **Actions** type has a value of 0x001F, formatting the instance will produce a string that contains "All". The other symbol strings won't appear.

So far, I've discussed how to convert numeric values into a string of flags. It's also possible to convert a string of comma-delimited symbols into a numeric value by calling **Enum**'s static **Parse** and **TryParse** methods. Here's some code demonstrating how to use these methods:

```csharp
// Because Query is defined as 8, 'a' is initialized to 8.
Actions a = (Actions) Enum.Parse(typeof(Actions), "Query", true);
Console.WriteLine(a.ToString());  // "Query"

// Because Query and Read are defined, 'a' is initialized to 9.
Enum.TryParse<Actions>("Query, Read", false, out a);
Console.WriteLine(a.ToString());  // "Read, Query"

// Creates an instance of the Actions enum with a value of 28
a = (Actions) Enum.Parse(typeof(Actions), "28", false);
Console.WriteLine(a.ToString());  // "Delete, Query, Sync"
```

When **Parse** and **TryParse** are called, the following actions are performed internally:

- 1. It removes all whitespace characters from the start and end of the string.
- 2. If the first character of the string is a digit, plus sign (+), or minus sign (-), the string is assumed to be a number, and an enum instance is returned whose numeric value is equal to the string converted to its numeric equivalent.

```csharp
public static FileAttributes Set(this FileAttributes flags, FileAttributes setFlags) {
    return flags | setFlags;
}

public static FileAttributes Clear(this FileAttributes flags,
    FileAttributes clearFlags) {
    return flags & ~clearFlags;
}

public static void ForEach(this FileAttributes flags,
    Action<FileAttributes> processFlag) {
    if (processFlag == null) throw new ArgumentNullException("processFlag");
    for (UInt32 bit = 1; bit != 0; bit <<= 1) {
        UInt32 temp = ((UInt32)flags) & bit;
        if (temp != 0) processFlag((FileAttributes)temp);
    }
}
```

And here is some code that demonstrates calling some of these methods. As you can see, the code looks as if I'm calling methods on the enumerated type:

```csharp
FileAttributes fa = FileAttributes.System;
fa = fa.Set(FileAttributes.ReadOnly);
fa = fa.Clear(FileAttributes.System);
fa.ForEach(f => Console.WriteLine(f));
```

## Chapter 16

## Arrays

**In this chapter:**

- Initializing Array Elements ... 388
- Casting Arrays ... 390
- All Arrays Are Implicitly Derived from System.Array ... 392
- All Arrays Implicitly Implement IEnumerable, ICollection, and IList ... 393
- Passing and Returning Arrays ... 394
- Creating Non-Zero–Lower Bound Arrays ... 395
- Array Access Performance ... 396
- Unsafe Array Access and Fixed-Size Array ... 401

Arrays are mechanisms that allow you to treat several items as a single collection. The Microsoft .NET common language runtime (CLR) supports single-dimensional arrays, multi-dimensional arrays, and jagged arrays (that is, arrays of arrays). All array types are implicitly derived from the **System.Array** abstract class, which itself is derived from **System.Object**. This means that arrays are always reference types that are allocated on the managed heap and that your application's variable or field contains a reference to the array and not the elements of the array itself. The following code shows how this is done:

```csharp
Int32[] myIntegers;                       // Declares a reference to an array
myIntegers = new Int32[100];              // Creates an array of 100 Int32s
```

On the first line, **myIntegers** is a variable that's capable of pointing to a single-dimensional array of **Int32**s. Initially, **myIntegers** will be set to **null** because I haven't allocated an array. The second line of code allocates an array of 100 **Int32** values; all of the **Int32**s are initialized to 0. Since arrays are reference types, the memory block required to hold the 100 unboxed **Int32**s is allocated on the managed heap. Actually, in addition to the array's elements, the memory block occupied by an array object also contains a type object pointer, a sync block index, and some additional overhead members as well. The address of this array's memory block is returned and saved in the variable **myIntegers**.

You can also create arrays of reference types:

```csharp
Control[] myControls;                     // Declares a reference to an array
myControls = new Control[50];             // Creates an array of 50 Control references
```

On the first line, **myControls** is a variable capable of pointing to a single-dimensional array of **Control** references. Initially, **myControls** will be set to **null** because I haven't allocated

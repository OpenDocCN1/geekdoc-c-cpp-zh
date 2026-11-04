
Three format strings are available on Enum methods that turn an enum value into a string. The default, G, prints the friendly name associated with the constant. To get the decimal or hexadecimal value, respectively, use D or X. Alternatively, we can use the System.Type of the enum type and leverage the Format method:

```
Console.WriteLine(Enum.Format(typeof(Color), value, "D"));
Console.WriteLine(Enum.Format(typeof(Color), value, "X"));
Console.WriteLine(Enum.Format(typeof(Color), value, "G"));
```

Yet another possibility is to use Enum.GetName, as follows:

```
Console.WriteLine(Enum.GetName(typeof(Color), value));
```

## Enumerating an Enum

Being an “enumerated series” of named constants, you might want to get all of an enum's defined members. Both GetNames and GetValues allow you to do so. Both will return an array with results, ordered by the binary values of the corresponding constants. If no aliases with the same value exist, both arrays will have equal length. The following code is used to print all the names and values available in an enum:

```
foreach (string member in Enum.GetNames(typeof(Color)))
    Console.WriteLine(member);

foreach (uint member in Enum.GetValues(typeof(Color)))
    Console.WriteLine(member);
```

Notice that the output of the preceding code will be Blue, Green, Red because of the value used for each of the enum constants. Because it's common to think of colors in terms of RGB values, it makes sense to list them in that order, despite their common hexadecimal representations growing in the opposite order.

If no duplicates exist, the following examples with LINQ's Zip operator can be used to get name/value pairs for an enum's members. The Zip and Cast methods used here are discussed in detail when we cover LINQ in Chapter 19, “Language Integrated Query Essentials.”

```
var res = Enum.GetNames(typeof(Color)).Zip(
    Enum.GetValues(typeof(Color)).Cast<uint>(),
    (name, value) => new { Name = name, Value = value }
);

// { Name = Blue, Value = 255 }
// { Name = Green, Value = 65280 }
// { Name = Red, Value = 16711680 }
foreach (var member in res)
    Console.WriteLine(member);
```

## Converting Integral Values to Enum Values

You learned how to turn an integral value back into an enum value, simply by using an explicit conversion. However, what happens if that integral value isn’t defined on the target enum type? Such a situation is likely to arise when such a value is retrieved from some persistent external storage (for example, the Registry, which can be tweaked by some administrator):

```csharp
uint value = 0xFF0001;
Color c = (Color)value;
Console.WriteLine(c);
```

The preceding code will just work fine and print the decimal representation of the color even though no enum member exists with the given value. When talking about flags enums, we see this may come in handy. However, if an enum defines a “discrete” domain of values (either this or that but not a combination of those), stricter checking might be desirable. Enter the IsDefined method of System.Enum that enables precisely this scenario:

```csharp
static void Main()
{
    PrintColor(0xFF0000);
    PrintColor(0xFF0001);  // Oops...
}

static void PrintColor(uint color)
{
    if (!Enum.IsDefined(typeof(Color), color))
        throw new ArgumentOutOfRangeException();

    Color c = (Color)color;
    Console.WriteLine(c);
}
```

Use of exceptions is the subject of Chapter 23, “Exceptions.” All you must remember from this example is the behavior of the IsDefined method, returning false if the specified value is not defined on the enum.

## Converting Strings to Enum Values

One final type of conversion is to start from a string representation like “Red” and go back to a corresponding enum value. Ignoring localization scenarios, this may be used to allow a user to enter a color “by name” while code wants to use the corresponding enum value on Color. Other uses include persistence based on a name rather than a value (which would allow enum values to change across versions of an application, though that’s still not recommended, especially if the enum type is publicly visible).

Both the Parse and TryParse methods can be used to achieve such a conversion. The latter method was introduced in .NET 4. Whereas the former method throws an exception if the string is not found as any of the enum's member names, the latter uses an output parameter and returns false if conversion fails. For flagged enums, which are discussed next, you can also pass in a comma-separated list of enum members that will make up the enum's value:

```csharp
Console.Write("Enter a color name: ");
var colorName = Console.ReadLine();

Color color;
if (!Enum.TryParse(colorName, /*ignoreCase*/ true, out color))
    Console.WriteLine("Color {0} doesn't exist.", colorName);
else
    Console.WriteLine(color);
```

Use of TryParse is recommended over Parse because invalid input is not too uncommon, and the expense (both in terms of processor cycles as well as code bloat) of exception handling to detect such input is high. Also because the TryParse method was introduced post-.NET 2.0, it can leverage generics to return the enum value in a strongly typed manner (rather than the System.Object return type on Enum.Parse).

## Flags

Besides their use for discrete named constants, enums can also be used to describe flags. For example, System.IO defines the FileMode enum as follows:

```csharp
public enum FileMode
{
    CreateNew = 1,
    Create = 2,
    Open = 3,
    OpenOrCreate = 4,
    Truncate = 5,
    Append = 6,
}
```

This nonflags enum is passed to APIs like File.Open to specify which mode to open the file with. Basically, this enum corresponds to Win32 constants passed to CreateFile. In fact, the values used for the different FileMode members directly map onto those used on the Win32 API being called. It's clear that something like FileMode describes a set of discrete values that are mutually exclusive. You can only "open" the file in any of the six available modes. Combining things such as Append with CreateNew doesn't make sense.

A similar nonflags enum is System.ConsoleKey, which contains key codes. Because it excludes values for modifier keys like Shift, Ctrl, and Alt, there's no meaning to combining multiple enum values. After all, you can't press A and B exactly at the same time; instead, your program will get to see each value one at a time in the order they were delivered by the input subsystem. Other examples include System.DayOfWeek because clearly it can't be both Monday and Wednesday at the same time (and place).

However, for lots of other enums, it makes sense to combine values. For example, the FileShare enum in the System.IO namespace does this. Can you tell the difference compared to the FileMode enum declaration?

```
[Flags]
public enum FileShare
{
    None = 0,
    Read = 1,
    Write = 2,
    ReadWrite = Read | Write,
    Delete = 4,
    Inheritable = 16,
}
```

By putting the Flags attribute on top of the enum, it becomes known as a flags enum whose values can be combined, typically using the | bitwise OR operator. For example, the ReadWrite entry in the preceding enum is built out of the combination of Read and Write. Its decimal value is 3, obtained from the bitwise OR (which coincides with the sum of the two values).

### Defining Flags Enums

Values of a flags enum are typically powers of two, except for auxiliary entries such as ReadWrite that associate a friendly name to a combination of flags. Wherever a flags enum is used, a combination of flags can be passed in by using the | operator. Whether certain combinations are meaningful for the target API is another question that should be addressed by providing proper documentation. For more information about the use of FileShare, refer to the MSDN documentation.

An equivalent way of looking at those flags enum values is to regard them as “values with exactly 1 bit set to 1” (which are powers of two). Each bit on the underlying type represents exactly one flag, and there’s no interference between flags in terms of the bits they use. This also shows why the underlying type may be of importance to you. For flags enums, it’s no longer the range of an integral value type that matters (such as the large range for uint, stretching from 0 to 4,294,967,295). Instead, the number of bits in the number matters (32 for a uint or int) and determines the maximum number of distinct flags that can be set by an enum value.

Use of a flags enum is often preferred over APIs that take a bunch of Boolean values as parameters to determine a modus operandi. For example, File.Open takes three enums, one of which is the FileShare flags enum:

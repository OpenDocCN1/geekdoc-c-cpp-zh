if the string is not found as any of the enum's member names, the latter uses an output parameter and returns false if conversion fails. For flagged enums, which are discussed next, you can also pass in a comma-separated list of enum members that will make up the enum's value:

```
```csharp
Console.Write("Enter a color name: ");
var colorName = Console.ReadLine();

Color color;
if (!Enum.TryParse(colorName, /*ignoreCase*/ true, out color))
    Console.WriteLine("Color {0} doesn't exist.", colorName);
else
    Console.WriteLine(color);
```
```

Use of TryParse is recommended over Parse because invalid input is not too uncommon, and the expense (both in terms of processor cycles as well as code bloat) of exception handling to detect such input is high. Also because the TryParse method was introduced post-.NET 2.0, it can leverage generics to return the enum value in a strongly typed manner (rather than the System.Object return type on Enum.Parse).

# ## Flags

Besides their use for discrete named constants, enums can also be used to describe flags. For example, System.IO defines the FileMode enum as follows:

```
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
```

This nonflags enum is passed to APIs like File.Open to specify which mode to open the file with. Basically, this enum corresponds to Win32 constants passed to CreateFile. In fact, the values used for the different FileMode members directly map onto those used on the Win32 API being called. It's clear that something like FileMode describes a set of discrete values that are mutually exclusive. You can only "open" the file in any of the six available modes. Combining things such as Append with CreateNew doesn't make sense.

A similar nonflags enum is System.ConsoleKey, which contains key codes. Because it excludes values for modifier keys like Shift, Ctrl, and Alt, there's no meaning to combining multiple enum values. After all, you can't press A and B exactly at the same time;
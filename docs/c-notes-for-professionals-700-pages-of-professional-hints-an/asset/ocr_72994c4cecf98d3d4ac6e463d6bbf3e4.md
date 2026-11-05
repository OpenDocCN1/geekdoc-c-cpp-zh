> "Do is on loop number 2."
> "Do is on loop number 3."
> "Do is on loop number 4."
> "Do is on loop number 5."

Unlike the while loop, the do-while loop is Exit Controlled. This means that the do-while loop would execute its statements at least once, even if the condition fails the first time.

```
bool a = false;
do
{
    Console.WriteLine("This will be printed once, even if a is false.");
} while (a == true);
```

# Section 52.60: long

The long keyword is used to represent signed 64-bit integers. It is an alias for the System.Int64 datatype present in mscorlib.dll, which is implicitly referenced by every C# project when you create them.

Any long variable can be declared both explicitly and implicitly:

```
long long1 = 9223372036854775806; // explicit declaration, long keyword used
var long2 = -9223372036854775806L; // implicit declaration, 'L' suffix used
```

A long variable can hold any value from −9,223,372,036,854,775,808 to 9,223,372,036,854,775,807, and can be useful in situations which a variable must hold a value that exceeds the bounds of what other variables (such as the int variable) can hold.

# Section 52.61: enum

The enum keyword tells the compiler that this class inherits from the abstract class Enum, without the programmer having to explicitly inherit it. Enum is a descendant of ValueType, which is intended for use with distinct set of named constants.

```
public enum DaysOfWeek
{
    Monday,
    Tuesday,
}
```

You can optionally specify a specific value for each one (or some of them):

```
public enum NotableYear
{
    EndOfWWI = 1918;
    EndOfWWII = 1945,
}
```

In this example I omitted a value for 0, this is usually a bad practice. An enum will always have a default value produced by explicit conversion (YourEnumType) 0, where YourEnumType is your declared enum type. Without a value of 0 defined, an enum will not have a defined value at initiation.

The default underlying type of enum is int, you can change the underlying type to any integral type including byte,
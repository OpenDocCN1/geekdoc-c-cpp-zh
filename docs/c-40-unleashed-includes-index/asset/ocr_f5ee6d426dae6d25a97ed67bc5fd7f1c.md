# Underlying Types

Because we’ve mentioned the word constant quite a bit, you might be wondering where enum members get their values. Moreover, what’s the type of those constant values? To answer those questions, we must introduce the notion of an underlying type that’s associated with an enum’s definition. The underlying type indicates the domain for the constants declared within the enum. If left unspecified, an enum’s underlying type is a 32-bit integer. You can specify the underlying type explicitly as shown here:

```
```text
enum Color : long
{
    Red,
    Green,
    Blue,
}
```
```

You’ll see this colon “derives from” syntax recurring quite a bit in Chapter 14 when we discuss inheritance. Permitted underlying types are integral numeric types such as byte, short, int, and long, together with their unsigned variants.

# Assigning Values to Members

What we haven’t explained yet is where the (constant) values for the enum’s members come from. Because we didn’t specify any values here, the enum will automatically get consecutive constant values for its members, starting from zero. So the definition of our Color enum is equivalent to the following:

```
```text
enum Color
{
    Red = 0,
    Green = Red + 1,
    Blue = Green + 1,
}
```
```

You can see those values by casting an enum value to the underlying type. Notice that calling ToString on an enum will actually print the symbolic name corresponding to the enum member:

```
```text
Color red = Color.Red;
Console.WriteLine(red);        // Prints "Red".
Console.WriteLine((int)red);   // Prints "0".
```
```

Instead of relying on the automatic numbering, you might want to supply values yourself, as shown here. This provides several advantages because you might want to use some relevant integral values that make sense in the target domain of the enum:
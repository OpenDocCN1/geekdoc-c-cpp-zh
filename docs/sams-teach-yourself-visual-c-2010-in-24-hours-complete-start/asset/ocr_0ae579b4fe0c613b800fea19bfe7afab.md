```
Thursday = Sunday + 4 ,
Friday = 5 ,
Saturday = 6 ,
```

Enumerations also support most of the standard operators that you can use on inte-ger values, although not all of them are actually meaningful. The most common operations you perform with enumerations are equality and inequality tests. Because enumerations are value types, you can declare a nullable enumeration as well.

# ## Did you Know?

# ### Underlying Enumeration Types

All the values contained in an enumeration must be of the same data type, called the **underlying type**. By default, the underlying type for enumerations is int, but any of the predefined integer types can be used: byte, short, int, long, sbyte, ushort, uint, or ulong.

To give your enumeration a different underlying type, you specify it after the identi-fier, like this:

```
enum Days : byte
{
   Sunday,
   Monday,
   Tuesday,
   Wednesday,
   Thursday,
   Friday,
   Saturday,
}
```

Keep in mind, however, that the underlying type determines the overall range of valid values you can choose from when defining the enumeration. In this case, the Days enumeration can have only values from 0 to 255.

# ### Try It Yourself

# ### Working with Enumerations

To implement the Days enumeration and explore how to use it, follow these steps. Keep Visual Studio open at the end of this exercise because you will use this appli-cation later.

+   1. Create a new Console application.

+   2. Add a new code file named Days.cs, and implement the Days enumeration.

+   3. In the Main method of the Program.cs file, declare a local variable of type Days named days and assign an initial value of Days.Sunday.
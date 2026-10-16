example, implicitly casting from a float to a double – float a = 3; double b = a;. The value assigned to a gets converted to a double automatically.

Then, because we cannot implicitly cast a double to a float so we need to do it explicitly – double a = 3; float b = (float)a;. The value in a can be converted into a float so long as it is explicitly stated that the conversion is being made.

+   - Creating a user-defined conversion requires you to follow this – static public implicit operator MagicNumber(int value) { /* your conversion is done here to return a MagicNumber */};

+   - To indicate the type of conversion you are doing, you can use the keywords, implicit or explicit.

# What's Next?

User-defined conversions are great features and used properly, they can turn your code into something easy to read and neat; and they are very powerful too.

In the next section, we look at extension methods, a C# feature that lets you add methods to classes that you never created and that you aren’t able to modify directly or add to. That will bring us to the end of this advanced section.
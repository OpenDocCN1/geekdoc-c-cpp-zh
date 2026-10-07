All sample code for this book has nullable enabled at the project level.

One last way to enable nullability is to set the project properties on the dotnet
command line with /p argument:

```
dotnet build /p:Nullable=enable
```

Specifying the value for Nullable on the command line will override any value set
in the project file.

# Implicitly Typed Local Variables

The contextual keyword var is used for declaring an implicitly typed local
variable. If code initializes a variable at declaration time with an expression of
unambiguous type, C# allows for the variable data type to be implied rather than
stated, as shown in Listing 3.3.

LISTING 3.3: Working with Strings

```
Console.Write("Enter text: ");
var text = Console.ReadLine();

// Return a new string in uppercase
var uppercase = text.ToUpper();

Console.WriteLine(uppercase);
```

This differs from Listing 2.18 in two ways. First, rather than using the
explicit data type string for the declaration, Listing 3.3 uses var. The resultant
CIL code is identical to using string explicitly. However, var indicates to the
compiler that it should infer the data type from the value assigned within the
declaration—in this case, the value returned by Console.ReadLine().

Second, the variables text and uppercase are initialized by their declarations.
Not doing so would result in an error at compile time. As mentioned earlier, the
compiler determines the data type of the initializing expression and declares the

+   4. Introduced in C# 3.0.
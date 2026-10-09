make the code more understandable, but it also verifies that the data type returned by the right-hand side expression is the type expected. When using a var-declared variable, the right-hand side data type should be obvious; if it isn’t, use of the var declaration should be avoided.

# Guidelines

**AVOID** using implicitly typed local variables unless the data type of the assigned value is obvious.

# Language Contrast: C++/Visual Basic/JavaScript—void*, Variant, and var

An implicitly typed variable is not the equivalent of void* in C++, a Variant in Visual Basic, or var in JavaScript. In each of these cases, the variable declaration is not very restrictive because the variable may be assigned a value of any type, just as can be done in C# with a variable declaration of type object. In contrast, var is definitely typed by the compiler; once established at declaration, the type may not change, and type checks and member calls are verified at compile time.

# ADVANCED TOPIC

# Anonymous Types

Support for var was added to the language in C# 3.0 to permit use of anonymous types. Anonymous types are data types that are declared “on the fly” within a method rather than through explicit class definitions, as shown in Listing 3.3. (See Chapter 15 for more details on anonymous types.)

# LISTING 3.3: Implicit Local Variables with Anonymous Types

```
class Program
{
    static void Main()
    {
        var patent1 =
            new { Title = "Bifocals",
                  YearOfPublication = "1784" };
        patent2 =
            new { Title = "Phonograph",
                  YearOfPublication = "1877" };
    }
}
```
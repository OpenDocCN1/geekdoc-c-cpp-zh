+   - Lambda expressions

+   - Query expressions

+   - Expression trees

+   - Automatic properties

+   - Object initializers

+   - Collection initializers

+   - Partial methods

Let's take a look at some details of these features.

# # Local Variable Type Inference

There are a few points in the C# language where you could say the syntax is “noisy”— developers have to type many characters to express their intention. For example, when you want to declare a local variable for a dictionary and immediately initialize it, you do it with some code similar to the following:

```
Dictionary<int, string> myCodeTable = new Dictionary<int, string>();
```

In this definition, writing the Dictionary<int, string> expression is twice as much as you could call syntax noise.

The local variable inference feature introduces the var context-sensitive keyword that reduces the noise, in this case shown:

```
var myCodeTable = new Dictionary<int, string>();
```

The var keyword can be used only for local variable declarations where the variable has an initialization expression. It is used as an “abbreviation”, and the compiler will generate exactly the same code as if you declared the myCodeTable as Dictionary<int, string>. When you declare a local variable with var, you actually tell the compiler, "Please parse the expression to the right of the equal sign and infer its type. I want your local variable declared with the type you've inferred."

You can use this of implicitly typed local variable declaration in for, foreach, and using statements, as well.

# # Extension Methods

Developers often write wrapper methods for objects that, in reality, could be the parts of the object itself. A good example is to check or not all characters in a string are in uppercase. This declaration can be put into a static helper class, just like in the following code extract:

```
public static class StringHelper
{
    public static bool IsUpper(string s) { ... }
}
```
+   - Default values must be constant values known at compile time. This means that you can set default values for parameters of types that C# considers to be primitive types, as shown in Table 5-1 in Chapter 5, “Primitive, Reference, and Value Types.” This also includes enumerated types, and any reference type can be set to `null`. For a parameter of an arbitrary value type, you can set the default value to be an instance of the value type, with all its fields containing zeroes. You can use the `default` keyword or the `new` keyword to express this; both syntaxes produce identical Intermediate Language (IL) code. Examples of both syntaxes are used by my M method for setting the default value for the `dt` parameter and `guid` parameter, respectively.

+   - Be careful not to rename parameter variables because any callers who are passing arguments by parameter name will have to modify their code. For example, in the declaration of my M method, if I rename the `dt` variable to `dateTime`, then my third call to M in the earlier code will cause the compiler to produce the following message: `error CS1739: The best overload for 'M' does not have a parameter named 'dt'.`

+   - Be aware that changing a parameter’s default value is potentially dangerous if the method is called from outside the module. A call site embeds the default value into its call. If you later change the parameter’s default value and do not recompile the code containing the call site, then it will call your method passing the old default value. You might want to consider using a default value of `0/null` as a sentinel to indicate default behavior; this allows you to change your default without having to recompile all the code with call sites. Here is an example.

```
```csharp
// Don't do this:
private static String MakePath(String filename = "Untitled") {
    return String.Format(@"{0}\{1}.txt", filename);
}

// Do this instead:
private static String MakePath(String filename = null) {
    // I am using the null-coalescing operator (??) here; see Chapter 19
    return String.Format(@"{0}\{1}.txt", filename ?? "Untitled");
}
```
```

+   - You cannot set default values for parameters marked with either the `ref` or `out` keywords because there is no way to pass a meaningful default value for these parameters.

There are some additional rules and guidelines that you should know about when calling a method by using optional or named parameters:

+   - Arguments can be passed in any order; however, named arguments must always appear at the end of the argument list.

+   - You can pass arguments by name to parameters that do not have default values, but all required arguments must be passed (by position or by name) for the compiler to compile the code.
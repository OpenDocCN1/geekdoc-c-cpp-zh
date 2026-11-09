+   - You can specify default values for the parameters of methods, constructor methods, and parameterful properties (C# indexers). You can also specify default values for parameters that are part of a delegate definition. Then, when invoking a variable of this delegate type, you can omit the arguments and accept the default values.

+   - Parameters with default values must come after any parameters that do not have default values. That is, once you define a parameter as having a default value, then all parameters to the right of it must also have default values. For example, in the definition of my M method, I would get a compiler error if I removed the default value ("A") for s. There is one exception to this rule: a params array parameter (discussed later in this chapter) must come after all parameters (including those that have default values), and the array cannot have a default value itself.

+   - Default values must be constant values known at compile time. This means that you can set default values for parameters of types that C# considers to be primitive types, as shown in Table 5-1 in Chapter 5, “Primitive, Reference, and Value Types.” This also includes enumerated types, and any reference type can be set to null. For a parameter of an arbitrary value type, you can set the default value to be an instance of the value type, with all its fields containing zeroes. You can use the default keyword or the new keyword to express this; both syntaxes produce identical Intermediate Language (IL) code. Examples of both syntaxes are used by M method for setting the default value for the dt parameter and guid parameter, respectively.

+   - Be careful not to rename parameter variables because any callers who are passing arguments by parameter name will have to modify their code. For example, in the declaration of my M method, if I rename the dt variable to dateTime, then my third call to M in the earlier code will cause the compiler to produce the following message: "error CS1739: The best overload for 'M' does not have a parameter named 'dt'."

+   - Be aware that changing a parameter’s default value is potentially dangerous if the method is called from outside the module. A call site embeds the default value into its call. If you later change the parameter’s default value and do not recompile the code containing the call site, then it will call your method passing the old default value. You might want to consider using a default value of 0/null as a sentinel to indicate default behavior; this allows you to change your default without having to recompile all the code with call sites. Here is an example:

```
```csharp
// Don’t do this:
private static String MakePath(String filename = "Untitled") {
    return String.Format(@"C:\{0}.txt", filename);
}

// Do this instead:
private static String MakePath(String filename = null) {
    // I am using the null-coalescing operator (??) here; see Chapter 19
    return String.Format(@"C:\{0}.txt", filename ?? "Untitled");
}
```
```

+   - You cannot set default values for parameters marked with either the ref or out keywords because there is no way to pass a meaningful default value for these parameters.
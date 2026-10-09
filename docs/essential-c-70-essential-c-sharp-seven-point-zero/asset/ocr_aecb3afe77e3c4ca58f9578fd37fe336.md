converts to a string, since many types support conversion to a string, and yet their underlying type is not a string.

While it might be clearer to check for null at the start of the method, in this case we check later to demonstrate that even if the target is null, the `is` operator will return false, and so the null check will still execute.

Note that with an explicit cast, it is the programmer’s responsibility to understand the code logic sufficiently to avoid an invalid cast exception. If there is the possibility of an invalid cast occurring, then it would be preferable to leverage an `is` operator and avoid the exception entirely. The advantage is that the `is` operator enables a code path for when the explicit cast might fail without the expense of exception handling.

Although the `is` operator capability is important, you should consider issues related to polymorphism prior to using the `is` operator. Polymorphism supports the expansion of a behavior to other data types without requiring any modification of the implementation that defines the behavior. For example, deriving from a common base type and then using that type as the parameter to the `Save( )` method avoids the need to check for string explicitly and enables other data types to support encryption during the save operation by deriving from the same base type.

# ## Pattern Matching with the `is` Operator

Starting with C# 7.0, the `is` operator has been improved to support a concept known as pattern matching. The problem with the `is` operator described previously is that after checking that data is indeed a string, we still must cast it to a string (assuming we want to access it as a string). A preferable approach would be to both check and, if the check is true, assign the result to a new variable. With C# 7.0’s introduction of **pattern matching**, this becomes possible, as shown in Listing 7.23. Effectively, the pattern-matching `is` operator replaces the more basic `is` operator in the vast majority of scenarios.

```
**LISTING 7.23: `is` Operator Determining the Underlying Type**

```csharp
public static void Save(object data)
{
    if (data is string text && text.Length > 0)
    {
        data = Encrypt(text);
        // ...
    }
}
```
```
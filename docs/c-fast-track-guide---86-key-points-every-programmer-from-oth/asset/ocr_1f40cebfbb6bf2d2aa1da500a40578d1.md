# 41. PROVIDING FALLBACK VALUES WITH ??

The null-coalescing operator ?? helps you safely assign fallback (default) values when a variable might be null.

Here’s how you can avoid null values by using ?? to supply a default value.

# [Code Example]

```
```csharp
// This variable might be null
string? userInput = null;

// Use ?? to provide a fallback value if userInput is null
string result = userInput ?? "Default Value";

// Print the result
Console.WriteLine(result);
```
```

# [Execution Result]

Default Value

In C#, a variable of a reference type (like string) can hold null, meaning "no value".

This can be risky—if you try to use a null value without checking, it can cause runtime errors (e.g., NullReferenceException).

The ?? operator solves this problem by letting you specify a "backup" value.

A ?? B means: if A is not null, use A; otherwise, use B.

This is extremely useful when you're dealing with user input, optional data, or data from uncertain sources.
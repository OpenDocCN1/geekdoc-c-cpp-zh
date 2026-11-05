```
```csharp
async Task<IEnumerable<string>> getEmailsFromFileAsync(string fileName)
{
    string text;

    using (StreamReader reader = File.OpenText(fileName))
    {
        text = await reader.ReadToEndAsync();
    }

    return from Match emailMatch in emailRegex.Matches(text) select emailMatch.Value;
}

async Task writeLinesToFileAsync(IEnumerable<string> lines, string fileName)
{
    using (StreamWriter writer = File.CreateText(fileName))
    {
        foreach (string line in lines)
        {
            await writer.WriteLineAsync(line);
        }
    }
}
```
```

One important thing that you may have noticed is that local functions can be defined under the `return` statement, they do **not** need to be defined above it. Additionally, local functions typically follow the "lowerCamelCase" naming convention as to more easily differentiate themselves from class scope functions.

# Section 71.3: out var declaration

A common pattern in C# is using `bool TryParse(object input, out object value)` to safely parse objects.

The `out var` declaration is a simple feature to improve readability. It allows a variable to be declared at the same time that it is passed as an out parameter.

A variable declared this way is scoped to the remainder of the body at the point in which it is declared.

# Example

Using TryParse prior to C# 7.0, you must declare a variable to receive the value before calling the function:

```
```csharp
Version < 7.0
int value;
if (int.TryParse(input, out value))
{
    Foo(value); // ok
}
else
{
    Foo(value); // value is zero
}

Foo(value); // ok
```
```

In C# 7.0, you can inline the declaration of the variable passed to the `out` parameter, eliminating the need for a separate variable declaration:

```
```csharp
Version ≥ 7.0
if (int.TryParse(input, out var value))
```
```
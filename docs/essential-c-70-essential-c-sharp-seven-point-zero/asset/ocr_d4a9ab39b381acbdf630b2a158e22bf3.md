# ### Chapter 2: Data Types

# TABLE 2.6: *string Methods (continued)*

| Statement | Example |
|---|---|
| `string ToLower()` | `string severity = "warning";` |
| `string ToUpper()` | `// Display the severity in uppercase` | `System.Console.WriteLine(severity.ToUpper());` |
| `string Trim()` | `// Remove any whitespace at the start or end` |
| `string Trim(...)` | `username = username.Trim();` |
| `string TrimEnd()` | |
| `string TrimStart()` | |
| `string Replace(` | `string filename;` |
| `string oldValue,` | `//...` |
| `string newValue)` | `// Remove 's from the string` | `filename = filename.Replace("?", "");` |

# ### ADVANCED TOPIC

# ## using Directive and using static Directive

The invocation of static methods as we have used them so far always involves a prefix of the namespace followed by the type name. When calling `System.Console.WriteLine`, for example, even though the method invoked is `WriteLine()` and there is no other method with that name within the context, it is still necessary to prefix the method name with the namespace (System) followed by the type name (Console). On occasion, you may want a shortcut to avoid such explicitness; to do so, you can leverage the C# 6.0 using static directive, as shown in Listing 2.15.

```
LISTING 2.15: using static Directive
```csharp
// The using directives allow you to drop the namespace
using static System.Console;
class HeyYou
{
    static void Main()
    {
        string firstName;
        string lastName;

        WriteLine("Hey you!");

        Write("Enter your first name: ");
        firstName = ReadLine();
```


```
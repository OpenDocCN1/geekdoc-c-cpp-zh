Like classes, namespaces support nesting. This provides for a hierarchical organization of classes. All the System classes relating to network APIs are in the namespace `System.Net`, for example, and those relating to the Web are in `System.Web`.

There are two ways to nest namespaces. The first approach is to nest them within one another (similar to classes), as demonstrated in Listing 9.14.

```
### LISTING 9.14: Nesting Namespaces within One Another

```csharp
// Define the namespace AddisonWesley
namespace AddisonWesley
{
    // Define the namespace AddisonWesley.Michaelis
    namespace Michaelis
    {
        // Define the namespace
        // AddisonWesley.Michaelis.EssentialCSharp
        namespace EssentialCSharp
        {
            // Declare the class
            // AddisonWesley.Michaelis.EssentialCSharp.Program
            class Program
            {
                // ...
            }
        }
    }
}
// End of AddisonWesley namespace declaration
```
```

Such a nesting will assign the `Program` class to the `AddisonWesley.Michaelis.EssentialCSharp` namespace.

The second approach is to use the full namespace in a single namespace declaration in which a period separates each identifier, as shown in Listing 9.15.

```
### LISTING 9.15: Nesting Namespaces Using a Period to Separate Each Identifier

```csharp
// Define the namespace AddisonWesley.Michaelis.EssentialCSharp
namespace AddisonWesley.Michaelis.EssentialCSharp
{
    class Program
    {
        // ...
    }
}
// End of AddisonWesley namespace declaration
```
```
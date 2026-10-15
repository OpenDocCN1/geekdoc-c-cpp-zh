a property or field call, the name may default to the name of the field or property rather than explicitly specifying the value. patent3, for example, is defined using a property named “Title” rather than an assignment to an explicit name. As Output 14.1 shows, the resultant property name is determined, by the compiler, to match the property from where the value was retrieved.

patent1 and patent2 both have the same property names with the same data types. Therefore, the C# compiler generates only one data type for these two anonymous declarations. patent3, however, forces the compiler to create a second anonymous type because the property name for the patent year is different from what it was in patent1 and patent2. Furthermore, if the order of the properties were switched between patent1 and patent2, these two anonymous types would also not be type-compatible. In other words, the requirements for two anonymous types to be type-compatible within the same assembly are a match in property names, data types, and order of properties. If these criteria are met, the types are compatible even if they appear in different methods or classes. Listing 14.2 demonstrates the type incompatibilities.

# LISTING 14.2: Type Safety and Immutability of Anonymous Types

```
class Program
{
    static void Main()
    {
        var patent1 =
            new
            {
                Title = "Bifocals",
                YearOfPublication = "1784"
            };

        var patent2 =
            new
            {
                YearOfPublication = "1877",
                Title = "Phonograph"
            };

        var patent3 =
            new
            {
                patent1.Title,
```
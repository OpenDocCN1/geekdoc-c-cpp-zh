```
// ...
}
```

Not only does PdaItem include the virtual modifier on the Name property, but Contact's Name property is also decorated with the keyword override. Eliminating virtual would result in an error and omitting override would cause a warning to be generated, as you will see shortly. C# requires the overriding methods to use the override keyword explicitly. In other words, virtual identifies a method or property as available for replacement (overriding) in the derived type.

# Language Contrast: Java and C++—Implicit Overriding

Unlike in Java and C++, the override keyword is required on the derived class in C#. C# does not allow implicit overriding. To override a method, both the base class and the derived class members must match and have corresponding virtual and override keywords. Furthermore, when the override keyword is specified, the derived implementation is assumed to replace the base class implementation.

Overriding a member causes the runtime to call the most derived implementation (see Listing 7.10 with Output 7.1).

# LISTING 7.10: Runtime Calling the Most Derived Implementation of a Virtual Method

```
public class Program
{
    public static void Main()
    {
        Contact contact;
        PdaItem item;

        contact = new Contact();
        item = contact;

        // Set the name via PdaItem variable
        item.Name = "Inigo Montoya";

        // Display that FirstName & LastName
```
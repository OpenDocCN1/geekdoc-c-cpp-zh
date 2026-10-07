Just as important to their appearance as regular methods is the fact that properties are an explicit construct within the CIL, too. As Listing 6.25 shows, the getters and setters are called by CIL properties, which are an explicit construct within the CIL code. Because of this, languages and compilers are not restricted to always interpreting properties based on a naming convention. Instead, CIL properties provide a means for compilers and code editors to provide special syntax.

# Listing 6.25: Properties Are an Explicit Construct in CIL

```
.property instance string FirstName()
{
    .get instance Program::FirstName()
    .set instance void Program::FirstName(string)
} // End of property Program:FirstName
```

Notice in Listing 6.24 that the getters and setters are part of the property include the specialName metadata. This modifier is what IDEs, such as Visual Studio, use as a flag to hide the members from IntelliSense.

An automatically implemented property is almost identical to one for which you define the backing field explicitly. In place of the manually defined backing field, the C# compiler generates a field with the name <PropertyName>k_BackingField in CIL. This generated field includes an attribute (see Chapter 18) called System.Runtime.CompilerServices.CompilerGeneratedAttribute. Both the getters and setters are decorated with the same attribute because they, too, are generated—with the same implementation as Listings 5.23 and 5.24.

# Constructors

Now that you have added fields to a class and can store data, you need to consider the validity of that data. As you saw in Listing 6.6, it is possible to instantiate an object using the new operator. The result, however, is the ability to create an employee with invalid data. Immediately following the assignment of employee,
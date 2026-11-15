# Output 5.5:

```
Inigo
```

The first thing to notice in Listing 5.17 is not the property code itself, but the code within the Program class. Although you no longer have the fields with the FirstName and LastName identifiers, you cannot see this by looking at the Program class. The API for accessing an employee's first and last names has not changed at all. It is still possible to assign the parts of the name using a simple assignment operator, for example (employee.First Name = "Inigo").

The key feature is that properties provide an API that looks programmatically like a field. In actuality, however, no such fields exist. A property declaration looks exactly like a field declaration, but following it are curly braces in which to place the property implementation. Two optional parts make up the property implementation. The get part defines the getter portion of the property. It corresponds directly to the GetFirstName() and GetLastName() functions defined in Listing 5.16. To access the FirstName property you call employee.FirstName. Similarly, setters (the set portion of the implementation) enable the calling syntax of the field assignment:

```
employee.FirstName = "Inigo";
```

Property definition syntax uses three contextual keywords. You use the get and set keywords to identify either the retrieval or the assignment portion of the property, respectively. In addition, the setter uses the value keyword to refer to the right side of the assignment operation. When Program.Main() calls employee.FirstName = "Inigo", therefore, value is set to "Inigo" inside the setter and can be used to assign _FirstName. Listing 5.17's property implementations are the most common. When the getter is called (such as in Console.WriteLine(employee2.FirstName)), the value from the field (_FirstName) is returned.

# Automatically Implemented Properties

In C# 3.0, property syntax includes a shorthand version. Since a property with a single backing field that is assigned and retrieved by the get and set
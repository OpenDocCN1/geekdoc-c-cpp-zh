# LINQ ENABLEING C# 3.0 LANGUAGE ENHANCEMENTS 21

these operators to each collection type individually, and custom collections of our own type would not benefit without intervention. Extension methods allow LINQ to apply equally to the built-in collection types, and any custom collection type, with the only requirement being the custom collection must implement IEnumerable<>. The current Microsoft-supplied extension methods and how to create new extension methods are covered in detail throughout this book. Understanding extension methods and how the built-in standard Query operators work will lead to a deeper understanding of how LINQ to Objects is built.

# Object Initializers

C# 3.0 introduced an object initialization shortcut syntax that allows a single C# statement to construct a new instance of a type and assign property values in one statement. While it is good programming practice to use constructor arguments for all critical data in order to ensure that a new type is stable and ready for use immediately after it is initialized (not allow to be instantiated into an invalid state), Object Initializers reduce the need to have a specific parameterized constructor for every variation of non-critical data argument set over time.

Listing 2-2 demonstrates the before and after examples of Object Initializers. Any field or property can be assigned in the initialization statement by assigning that property name to a value; multiple assignments can be made by separating the expressions with a comma. The C# compiler behind the scenes calls the default constructor of the object and then calls the individual assignment statements as if you had previously assigned properties in subsequent statements manually. (See the C# 3.0 Language Specification in endnote 2 for a more precise description of how this initialization actually occurs.)

# Listing 2-2 Object Initializer syntax–before and after

```
// old initialization syntax => multiple statements
contactOld = new Contact();
contactOld.LastName = "Magennis"
contactOld.DateOfBirth = new DateTime(1973, 12, 09);

// new initialization syntax => single statement
contact contactNew = new Contact
{
    LastName = "Magennis"
    DateOfBirth = new DateTime(1973, 12, 09)
};
```
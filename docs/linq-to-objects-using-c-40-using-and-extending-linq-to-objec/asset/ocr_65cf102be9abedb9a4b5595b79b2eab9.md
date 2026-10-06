# Projecting Grouped Elements into a New Type

The general group by function when using query syntax returns returns the same element type as the source collection elements. The workaround is to use query continuation, which is discussed later in the chapter.) If you would like the grouped elements to be in a different form, you must use the extension method syntax and specify your own "element selector" expression. The element selector takes an instance of the original element and returns a new type based on the supplied expression.

Listing 4-7 demonstrates how to group records by state and return a group of strings rather than a group of Contact instances for each element (Contact is the original element type). In this case, a string is returned by concatenating the contact's first and last name. The Console output result is shown in Output 4-4.

Listing 4-7 Group elements can be projected to any type. This sample projects elements as a string type, rather than the default Contact instance—see Output 4-4

```
IList<Contact> contacts = Contact.SampleData();
```

```
var q = contacts.GroupBy(
    c => c.State,
    c => c.FirstName + " " + c.LastName
);

foreach (var group in q)
{
    Console.WriteLine("State: {0}", group.Key);
    foreach (string name in group)
        Console.WriteLine("{0}", name);
}
```

# Output 4-4

State: CA
Barney Gottshall
Mandy Gottshall
Anthony Gauwain
Jeffery Deane
State: WA
Bernadette Gottshall
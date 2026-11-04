# Part I: C# Fundamentals

The output shows that once the query is executed, its value does not change:

```
First execution
----------------
Count: 5
Second execution
----------------
Count: 5
```

# LINQ and Anonymous Types

Although Chapter 4 explored anonymous types and how they allow you to define data types without having to formally define a class, you have not yet seen their real use. In fact, anonymous type is another new feature that Microsoft has designed with LINQ in mind.

Consider the following Contact class definition:

```
public class Contact
{
    public int id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
}
```

Suppose that you have a list containing Contact objects, like this:

```
List<Contact> Contacts = new List<Contact>() {
    new Contact() { id = 1, FirstName = "John", LastName = "Chen" },
    new Contact() { id = 2, FirstName = "Maryann", LastName = "Chen" },
    new Contact() { id = 3, FirstName = "Richard", LastName = "Wells" }
};
```

You can use LINQ to query all contacts with Chen as the last name:

```
IEnumerable<Contact> foundContacts = from c in Contacts
                                      where c.LastName == "Chen"
                                      select c;
```

The foundContacts object is of type IEnumerable<Contact>. To print out all the contacts in the result, you can use the foreach loop:

```
foreach (var c in foundContacts)
{
    Console.WriteLine("{0} - {1} {2}", c.id, c.FirstName, c.LastName);
}
```

The output looks like this:

```
1 - John Chen
2 - Maryann Chen
```
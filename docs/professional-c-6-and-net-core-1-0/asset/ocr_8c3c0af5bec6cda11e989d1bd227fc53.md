NOTE Arrays are explained in Chapter 7.

The CustomIndexerSample makes use of these dependencies and namespaces:

# Dependencies

NETStandard.Library

# Namespaces

+   - System
+   - System.Collections.Generic
+   - System.Linq
+   - static System.Console

To create a custom indexer, first create a Person class with read-only properties FirstName, LastName, and Birthday (code file CustomIndexerSample/Person.cs):

```
public class Person
{
    public DateTime Birthday { get; }
    public string FirstName { get; }
    public string LastName { get; }

    public Person(string firstName, string lastName, DateTime birthDay)
    {
        FirstName = firstName;
        LastName = lastName;
        Birthday = birthDay;
    }

    public override string ToString() => $"{FirstName} {LastName}";
}
```

The class PersonCollection defines a private array field that contains Person elements and a constructor where a number of Person objects can be passed (code file CustomIndexerSample/PersonCollection.cs):

```
public class PersonCollection
{
    private Person[] _people;

    public PersonCollection(params Person[] people)
    {
        _people = people.ToArray();
    }
}
```

For allowing indexer-syntax to be used to access the PersonCollection and return Person objects, you can create an indexer. The indexer looks very similar to a property as it also contains get and set accessors. What’s different is the name. Specifying an indexer makes use of the this keyword. The brackets that follow the this keyword specify the
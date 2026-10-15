```
public class Contact : PdaItem, IPerson
{
    private Person Person
    {
        get { return _Person; }
        set { _Person = value; }
    }
    private Person _Person;

    public string FirstName
    {
        get { return _Person.FirstName; }
        set { _Person.FirstName = value; }
    }

    public string LastName
    {
        get { return _Person.LastName; }
        set { _Person.LastName = value; }
    }

    // ...
}
```

IPerson ensures that the signatures between the Person members and the same members duplicated onto Contact are consistent. The implementation is still not synonymous with multiple inheritance, however, because new members added to Person will not be added to Contact.

One possible improvement that works if the implemented members are methods (not properties) is to define interface extension methods for the additional functionality “derived” from the second base class. An extension method on IPerson could provide a method called VerifyCredentials(), for example, and all classes that implement IPerson—even an IPerson interface that had no members but just extension methods—would have a default implementation of VerifyCredentials(). What makes this approach viable is the fact that polymorphism is still available, as is overriding. Overriding is supported because any instance implementation of a method will take priority over an extension method with the equivalent static signature.

# Guidelines

CONSIDER defining interfaces to achieve a similar effect to that of multiple inheritance.
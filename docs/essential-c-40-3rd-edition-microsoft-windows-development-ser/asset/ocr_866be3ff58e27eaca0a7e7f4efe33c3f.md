# LISTING 6.17: Specifying Which Base Constructor to Invoke

```
public class PdaItem
{
    public PdaItem(string name)
    {
        Name = name;
    }

    // ...
}
```

```
public class Contact : PdaItem
{
    public Contact(string name) :
        base(name)
    {
        Name = name;
    }

    public string Name { get; set; }

    // ...
}
```

By identifying the base constructor in the code, you let the runtime know which base constructor to invoke before invoking the derived class constructor.

# Abstract Classes

Many of the inheritance examples so far have defined a class called PdaItem that defines the methods and properties common to Contact, Appointment, and so on, which are type objects that derive from PdaItem. PdaItem is not intended to be instantiated itself, however. A PdaItem instance has no meaning by itself; it has meaning only when it is used as a base class—to share default method implementations across the set of data types that derive from it. These characteristics are indicative of the need for PdaItem to be an abstract class rather than a concrete class. Abstract classes are designed for derivation only. It is not possible to instantiate an abstract class, except in the context of instantiating a class that derives from it. Classes that are not abstract and can instead be instantiated directly are concrete classes.
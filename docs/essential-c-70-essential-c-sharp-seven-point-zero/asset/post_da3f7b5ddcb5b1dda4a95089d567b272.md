
## protected Access Modifier

  Encapsulation is finer grained than just public or private, however. It is possible to define members in base classes that only derived classes can access. As an example, consider the ObjectKey property shown in Listing 7.7.

### LISTING 7.7: protected Members Are Accessible Only from Derived Classes

```csharp
public class Program
{
    public static void Main()
    {
        Contact contact = new Contact();
        contact.Name = "Inigo Montoya";

        // ERROR: 'PdaItem.ObjectKey' is inaccessible
        // due to its protection level
        // contact.ObjectKey = Guid.NewGuid();
    }
}

public class PdaItem
{
    protected Guid ObjectKey { get; set; }
    // ... 
}

public class Contact : PdaItem
{
    void Save()
    {
        // Instantiate a FileStream using <ObjectKey>.dat
        // for the filename
        FileStream stream = System.IO.File.OpenWrite(
            ObjectKey + ".dat");
    }

    void Load(PdaItem pdaItem)
    {
        // ERROR: 'pdaItem.ObjectKey' is inaccessible
        // due to its protection level
        // pdaItem.ObjectKey = ...;

        Contact contact = pdaItem as Contact;
        if(contact != null)
        {
            contact.ObjectKey = ...;
        }
        // ... 
    }
}
```

  ObjectKey is defined using the protected access modifier. The result is that it is accessible outside of PdaItem only from classes that derive from PdaItem. Contact derives from PdaItem, so all members of Contact have access to ObjectKey. In contrast, Program does not derive from PdaItem, so using the ObjectKey property within Program results in a compile-time error.

> **NOTE**
> Protected members in the base class are accessible only from the base class and other classes within the derivation chain.

  A subtlety shown in the Contact.Load( ) method is worth noting. Developers are often surprised that it is not possible to access the protected ObjectKey of an explicit PdaItem from code within Contact, even though Contact derives from PdaItem. The reason is that a PdaItem could potentially be an Address, and Contact should not be able to access protected members of Address. Therefore, encapsulation prevents Contact from potentially modifying the ObjectKey of an Address. A successful cast to Contact will bypass the restriction as shown. The governing rule is that accessing a protected member from a derived class requires compile-time determination that the protected member is an instance of the derived class (or a class further derived from it).

## Extension Methods

  Extension methods are technically not members of the type they extend and therefore are not inherited. Nevertheless, because every derived class may be used as an instance of any of its base classes, an extension method on one type also extends every derived type. If we extend a base class such as PdaItem, all the extension methods will also be available in the derived classes. However, as with all extension methods, priority is given to instance methods. If a compatible signature appears anywhere within the inheritance chain, it will take precedence over an extension method.

  Requiring extension methods on base types is rare. As with extension methods in general, if the base type's code is available, it is preferable to modify the base type directly. Even in cases where the base type's code is unavailable, programmers should consider whether to add extension methods to an interface that the base type or individual derived types implement. We cover interfaces and how to use them with extension methods in the next chapter.

## Single Inheritance

  In theory, you can place an unlimited number of classes in an inheritance tree. For example, Customer derives from Contact, which derives from PdaItem, which derives from object. However, C# is a single-inheritance programming language (as is the CIL language to which C# compiles). This means that a class cannot derive from two classes directly. It is not possible, for example, to have Contact derive from both PdaItem and Person.

### Language Contrast: C++—Multiple Inheritance

  C#’s single inheritance is one of its major object-oriented differences from C++.

  For the rare cases that require a multiple-inheritance class structure, one solution is to use aggregation; instead of one class inheriting from another, one class contains an instance of the other. Figure 7.2 shows an example of this class structure. Aggregation occurs when the association relationship defines a core part of the containing object. For multiple inheritance, this involves picking one class as the primary base class (PdaItem) and deriving a new class (Contact) from that. The second desired base class (Person) is added as a field in the derived class (Contact). Next, all the nonprivate members on the field (Person) are redefined on the derived class (Contact), which then delegates the calls out to the field (Person). Some code duplication occurs because methods are redeclared; however, this is minimal, since the real method body is implemented only within the aggregated class (Person).

  In Figure 7.2, Contact contains a private property called InternalPerson that is drawn as an association to the Person class. Contact also contains the FirstName and LastName properties but with no corresponding fields. Instead, the FirstName and LastName properties simply delegate their calls out to `InternalPerson.FirstName` and `InternalPerson.LastName`, respectively. Listing 7.8 shows the resultant code.

![](img/ef6a8a417630b222bfb3f3b949facff0_360_0.png)

**FIGURE 7.2: SIMULATING MULTIPLE INHERITANCE USING AGGREGATION**

### LISTING 7.8: WORKING AROUND SINGLE INHERITANCE USING AGGREGATION

```csharp
public class PdaItem
{
    // ...
}

public class Person
{
    // ...
}

public class Contact : PdaItem
{
    private Person InternalPerson { get; set; }

    public string FirstName
    {
        get { return InternalPerson.FirstName; }
        set { InternalPerson.FirstName = value; }
    }

    public string LastName
    {
        get { return InternalPerson.LastName; }
        set { InternalPerson.LastName = value; }
    }

    // ...
}
```

  Besides the added complexity of delegation, another drawback is that any methods added to the field class (Person) will require manual addition to the derived class (Contact); otherwise, Contact will not expose the added functionality.

## Sealed Classes

  To design a class correctly that others can extend via derivation can be a tricky task that requires testing with examples to verify the derivation will work successfully. Listing 7.9 shows how to avoid unexpected derivation scenarios and problems by marking classes as sealed.

### LISTING 7.9: Preventing Derivation with Sealed Classes

```csharp
public sealed class CommandLineParser
{
    // ...
}

// ERROR: Sealed classes cannot be derived from
public sealed class DerivedCommandLineParser :
    CommandLineParser
{
    // ...
}
```

  Sealed classes include the sealed modifier, and the result is that they cannot be derived from. The string type is an example of a type that uses the sealed modifier to prevent derivation.

## Overriding the Base Class

  All members of a base class are inherited in the derived class, except for constructors and destructors. However, sometimes the base class does not have the optimal implementation of a particular member. Consider the `Name` property on `PdaItem`, for example. The implementation is probably acceptable when inherited by the `Appointment` class. For the `Contact` class, however, the `Name` property should return the `FirstName` and `LastName` properties combined. Similarly, when `Name` is assigned, it should be split across `FirstName` and `LastName`. In other words, the base class property declaration is appropriate for the derived class, but the implementation is not always valid. There needs to be a mechanism for **overriding** the base class implementation with a custom implementation in the derived class.

### *virtual* Modifier

  C# supports overriding on instance methods and properties but not on fields or on any static members. It requires an explicit action within both the base class and the derived class. The base class must mark each member for which it allows overriding as `virtual`. If `public` or `protected` members do not include the `virtual` modifier, subclasses will not be able to override those members.

> **Language Contrast:** Java---Virtual Methods by Default
> By default, methods in Java are virtual, and they must be explicitly sealed if nonvirtual behavior is preferred. In contrast, C# defaults to nonvirtual.

  Listing 7.10 shows an example of property overriding.

### LISTING 7.10: Overriding a Property

```csharp
public class PdaItem
{
    public virtual string Name { get; set; }
    // ...
}
```

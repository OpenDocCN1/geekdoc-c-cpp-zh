
Internal state changes mean that it’s possible to violate object invariants, at least temporarily. After you have replaced the City field, you have placed a1 in an invalid state. The city has changed and no longer matches the state or ZIP code fields. The code looks harmless enough, but suppose that this fragment is part of a multithreaded program. Any context switch after the city changes and before the state changes would leave the potential for another thread to see an inconsistent view of the data.

Okay, so you think you’re not writing a multithreaded program. You can still get into trouble. Imagine that the ZIP code was invalid and the set threw an exception. You’ve made only some of the changes you intended, and you’ve left the system in an invalid state. To fix this problem, you would need to add considerable internal validation code to the address structure. That validation code would add considerable size and complexity. To fully implement exception safety, you would need to create defensive copies around any code block in which you change more than one field. Thread safety would require adding significant thread-synchronization checks on each property accessor, both sets and gets. All in all, it would be a significant undertaking—and one that would likely be extended over time as you add new features.

Instead, if you need Address to be a struct, make it immutable. Start by changing all instance fields to read-only for outside uses.

```
public struct Address2
{
    // remaining details elided
    public string Line1
    {
        get;
        private set;
    }
    public string Line2
    {
        get;
        private set;
    }
    public string City
    {
        get;
        private set;
    }
    public string State
    {
        get;
        private set;
    }
    public int ZipCode
    {
        get;
        private set;
    }
}
```

Now you have an immutable type, based on the public interface. To make it useful, you need to add all necessary constructors to initialize the Address structure completely. The Address structure needs only one additional constructor, specifying each field. A copy constructor is not needed because the assignment operator is just as efficient. Remember that the default constructor is still accessible. There is a default address where all the strings are null, and the ZIP code is 0:

```
public Address2(string line1,
    string line2,
    string city,
    string state,
    int zipCode) :
    this()
{
    Line1 = line1;
    Line2 = line2;
    City = city;
    ValidateState(state);
    State = state;
    ValidateZip(zipCode);
    ZipCode = zipCode;
}
```

Using the immutable type requires a slightly different calling sequence to modify its state. You create a new object rather than modify the existing instance:

```
// Create an address:
Address2 a2 = new Address2("111 S. Main",
    "", "Anytown", "IL", 61111);
```

```
// To change, re-initialize:
a2 = new Address2(a1.Line1,
    a1.Line2, "Ann Arbor", "MI", 48103);
```

The value of a1 is in one of two states: its original location in Anytown, or its updated location in Ann Arbor. You do not modify the existing address to create any of the invalid temporary states from the previous example. Those interim states exist only during the execution of the Address constructor and are not visible outside that constructor. As soon as a new Address object is constructed, its value is fixed for all time. It’s exception safe: a1 has either its original value or its new value. If an exception is thrown during the construction of the new Address object, the original value of a1 is unchanged.

This second Address type is not strictly immutable. Implicit Properties with private setters can still contain methods that change the internal state. If you want a truly immutable type, you would need to make further changes. You need to change the implicit properties to explicit properties, and change the backing field to a readonly field of the type:

```
public struct Address3
{
    // remaining details elided
    public string Line1
    {
        get { return Line1; }
    }
    private readonly string line1;

    public string Line2
    {
        get { return line2; }
    }
    private readonly string line2;

    public string City
    {
        get { return city; }
    }
    private readonly string city;
    
    public string State
    {
        get { return state; }
    }
    private readonly string state;
    
    public int ZipCode
    {
        get { return zip; }
    }
    private readonly int zip;
    
    public Address3(string line1,
        string line2,
        string city,
        string state,
        int zipCode) :
    {
        this.line1 = line1;
        this.line2 = line2;
        this.city = city;
        ValidateState(state);
        this.state = state;
        ValidateZip(zipCode);
        this.zip = zipCode;
    }
}
```

To create an immutable type, you need to ensure that there are no holes that would allow clients to change your internal state. Value types do not support derived types, so you do not need to defend against derived types modifying fields. But you do need to watch for any fields in an immutable type that are mutable reference types. When you implement your constructors for these types, you need to make a defensive copy of that mutable type. All these examples assume that Phone is an immutable value type because we're concerned only with immutability in value types:

```
// Almost immutable: there are holes that would
// allow state changes.
public struct PhoneList
{
    private readonly Phone[] phones;

    public PhoneList(Phone[] ph)
    {
        phones = ph;
    }

    public IEnumerable<Phone> Phones
    {
        get
        {
            return phones;
        }
    }
}

Phone[] phones = new Phone[10];
// initialize phones
PhoneList pl = new PhoneList(phones);

// Modify the phone list:
// also modifies the internals of the (supposedly)
// immutable object.
phones[5] = Phone.GeneratePhoneNumber();
```

The array class is a reference type. The array referenced inside the PhoneList structure refers to the same array storage (phones) allocated outside the object. Developers can modify your immutable structure through another variable that refers to the same storage. To remove this possibility, you need to make a defensive copy of the array. The previous example shows the pitfalls of a mutable collection. Even more possibilities for mischief exist if the Phone type is a mutable reference type. Clients could modify the values in the collection, even if the collection is protected against any modification. This defensive copy should be made in all constructors whenever your immutable type contains a mutable reference type:

```
// Immutable: A copy is made at construction.
public struct PhoneList2
{
    private readonly Phone[] phones;

    public PhoneList2(Phone[] ph)
    {
        phones = new Phone[ph.Length];
        // Copies values because Phone is a value type.
        ph.CopyTo(phones, 0);
    }

    public IEnumerable<Phone> Phones
    {
        get
        {
            return phones;
        }
    }
}

Phone[] phones2 = new Phone[10];
// initialize phones
PhoneList p2 = new PhoneList(phones);

// Modify the phone list:
// Does not modify the copy in pl.
phones2[5] = Phone.GeneratePhoneNumber();
```

You need to follow the same rules when you return a mutable reference type. If you add a property to retrieve the entire array from the PhoneList struct, that accessor would also need to create a defensive copy. See Item 27 for more details.

The complexity of a type dictates which of three strategies you will use to initialize your immutable type. The Address structure defined one constructor to allow clients to initialize an address. Defining the reasonable set of constructors is often the simplest approach.

You can also create factory methods to initialize the structure. Factories make it easier to create common values. The .NET Framework Color type follows this strategy to initialize system colors. The static methods `Color.FromKnownColor()` and `Color.FromName()` return a copy of a color value that represents the current value for a given system color.

Third, you can create a mutable companion class for those instances in which multistep operations are necessary to fully construct an immutable type. The .NET string class follows this strategy with the System.Text.StringBuilder class. You use the StringBuilder class to create a string using multiple operations. After performing all the operations necessary to build the string, you retrieve the immutable string from the StringBuilder.

Immutable types are simpler to code and easier to maintain. Don’t blindly create get and set accessors for every property in your type. Your first choice for types that store data should be immutable, atomic value types. You easily can build more complicated structures from these entities.

```
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
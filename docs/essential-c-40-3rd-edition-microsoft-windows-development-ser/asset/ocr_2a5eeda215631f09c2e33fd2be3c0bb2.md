```
public string City;
public string State;
public string Zip;

public override string ToString()
{
    return string.Format("{0}" + Environment.NewLine +
        "{1}, {2} {3}",
        StreetAddress, City, State, Zip);
}
```

```
public class InternationalAddress : Address
{
    public string Country;

    public override string ToString()
    {
        return base.ToString() + Environment.NewLine +
            Country;
    }
}
```

In Listing 6.16, InternationalAddress inherits from Address and implements ToString(). To call the parent class's implementation you use the base keyword. The syntax is virtually identical to this, including support for using base as part of the constructor (discussed shortly).

Parenthetically, in the Address.ToString() implementation, you are required to override as well because ToString() is also a member of object. Any members that are decorated with override are automatically designated as virtual, so additional child classes may further specialize the implementation.

# Constructors

When instantiating a derived class, the runtime first invokes the base class's constructor so that the base class initialization is not circumvented. However, if there is no accessible (nonprivate) default constructor on the base class, then it is not clear how to construct the base class and the C# compiler reports an error.

To avoid the error caused by no accessible default constructor, programmers need to designate explicitly, in the derived class constructor header, which base constructor to run (see Listing 6.17).
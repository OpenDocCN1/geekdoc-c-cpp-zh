In fact, the compiler transforms the code shown in Listing 3.2 into code that looks roughly like that shown in Listing 3.3.

# **LISTING 3.3  Declaring a Property**

```
class Contact
{
    private string firstName;

    public string FirstName
    {
        get
        {
            return this.firstName;
        }
        set
        {
            this.firstName = value;
        }
    }
}
```

![](bbox=[0.058, 0.455, 0.186, 0.491])

# **Automatic Properties**

Automatic properties are convenient, especially when you implement a large number of properties. This convenience does come at a slight cost, however.

Because you don’t provide a body for the accessors, you can’t specify any logic that executes as part of that accessor, and both accessors must be declared using the automatic property syntax. As a result, if at some point later you realize that you need to provide logic for either of the accessors, you need to add a backing field and the appropriate logic to both accessors.

Fortunately, this change doesn’t affect the public interface of your class, so it is safe to make, although it might be a bit tedious.

The get accessor uses a return statement, which simply instructs the accessor to return the value indicated. In the set accessor of the code in Listing 3.3, the class field firstName is set equal to value, but where does value come from? From Table 1.6 in Chapter 1, you know that value is a contextual keyword. When used in a property set accessor, the value keyword always means “the value that was provided by the caller” and is always typed to be the same as the property type.

By default, the property accessors inherit the accessibility declared on the property definition itself. You can, however, declare a more restrictive accessibility for either the get or the set accessor.
```
#region IListable Members
string[] IListable.ColumnValues
{
    get
    {
        return new string[]
        {
            FirstName,
            LastName,
            Phone,
            Address
        };
    }
}
#endregion
}
```

Listing 8.5 implements ColumnValues explicitly by prefixing the property name with IListable. Furthermore, since explicit interface implementations are directly associated with the interface, there is no need to modify them with virtual, override, or public. In fact, these modifiers are not allowed. The method is not treated as a public member of the class, so marking it as public would be misleading.

# Implicit Member Implementation

Notice that CompareTo( ) in Listing 8.5 does not include the IComparable prefix; it is implemented implicitly. With implicit member implementation, it is necessary only for the member to be public and for the member’s signature to match the interface member’s signature. Interface member implementation does not require use of the override keyword or any indication that this member is tied to the interface. Furthermore, since the member is declared just like any other class member, code that calls implicitly implemented members can do so directly, just as it would any other class member:

```
result = contact1.CompareTo(contact2);
```

In other words, implicit member implementation does not require a cast because the member is not hidden from direct invocation on the implementing class.

Many of the modifiers disallowed on an explicit member implementation are required or are optional on an implicit implementation. For example, implicit member implementations must be public. Furthermore,
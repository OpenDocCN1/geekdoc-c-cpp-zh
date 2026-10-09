Each interface member behaves like an abstract method, forcing the derived class to implement the member. Therefore, it is not possible to use the abstract modifier on interface members explicitly.

When implementing an interface member in a type, there are two ways to do so: **explicitly or implicitly**. So far we've seen only implicit implementations, where the type member that implements the interface member is a public member of the implementing type.

# Explicit Member Implementation

Explicitly implemented methods are available only by calling them through the interface itself; this is typically achieved by casting an object to the interface. For example, to call `IListable.ColumnValues` in Listing 8.4, you must first cast the contact to `IListable` because of `ColumnValues'` explicit implementation.

# **LISTING 8.4: Calling Explicit Interface Member Implementations**

```
```csharp
string[] values;
Contact contact1, contact2;

// ...

// ERROR: Unable to call ColumnValues() directly
// on a contact
// values = contact1.ColumnValues;

// First cast to IListable
values = ((IListable)contact2).ColumnValues;
// ...
```
```

The cast and the call to `ColumnValues` occur within the same statement in this case. Alternatively, you could assign `contact2` to an `IListable` variable before calling `ColumnValues`.

To declare an explicit interface member implementation, prefix the member name with the interface name (see Listing 8.5).

# **LISTING 8.5: Explicit Interface Implementation**

```
```csharp
public class Contact : PdaItem, IListable, IComparable
{
    // ...

    public int CompareTo(object obj)
    {
        // ...
    }
} 
```
```
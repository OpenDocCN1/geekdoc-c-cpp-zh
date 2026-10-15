
Each interface member behaves like an abstract method, forcing the derived class to implement the member. Therefore, it is not possible to use the abstract modifier on interface members explicitly.

When implementing an interface member in a type, there are two ways to do so: explicitly or implicitly. So far we’ve seen only implicit implementations, where the type member that implements the interface member is a public member of the implementing type.

## Explicit Member Implementation

Explicitly implemented methods are available only by calling them through the interface itself; this is typically achieved by casting an object to the interface. For example, to call `IListable.ColumnValues` in Listing 7.4, you must first cast the contact to `IListable` because of ColumnValues’ explicit implementation.

```
Listing 7.4: Calling Explicit Interface Member Implementations

```csharp
string[] values;
Contact contact1, contact2;

// ...

// ERROR:  Unable to call ColumnValues() directly
//         on a contact.
// values = contact1.ColumnValues;

// First cast to IListable.
values = ((IListable)contact2).ColumnValues;
// ...
```
```

The cast and the call to ColumnValues occur within the same statement in this case. Alternatively, you could assign contact2 to an IListable variable before calling ColumnValues.

To declare an explicit interface member implementation, prefix the member name with the interface name (see Listing 7.5).

```
Listing 7.5: Explicit Interface Implementation

```csharp
public class Contact : PdaItem, IListable, IComparable
{
    // ...

    public int CompareTo(object obj)
    {
```

```
// ...
}
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

Listing 7.5 implements ColumnValues explicitly by prefixing the property name with IListable. Furthermore, since explicit interface implementations are directly associated with the interface, there is no need to modify them with virtual, override, or public. In fact, these modifiers are not allowed. The method is not treated as a public member of the class, so marking it as public would be misleading.

## Implicit Member Implementation

Notice that CompareTo() in Listing 7.5 does not include the IComparable prefix; it is implemented implicitly. With implicit member implementation, it is necessary only for the member to be public and for the member’s signature to match the interface member’s signature. Interface member implementation does not require use of the override keyword or any indication that this member is tied to the interface. Furthermore, since the member is declared just like any other class member, code that calls implicitly implemented members can do so directly, just as it would any other class member:

```
result = contact1.CompareTo(contact2);
```

In other words, implicit member implementation does not require a cast because the member is not hidden from direct invocation on the implementing class.

Many of the modifiers disallowed on an explicit member implementation are required or are optional on an implicit implementation. For example, implicit member implementations must be public. Furthermore, virtual is optional depending on whether derived classes may override the implementation. Eliminating virtual will cause the member to behave as though it is sealed.

## Explicit versus Implicit Interface Implementation

The key difference between implicit and explicit member interface implementation lies not in the syntax of the method declaration, but rather in the ability to access the method by name through an instance of the type rather than via the interface.

When building a class hierarchy, it’s desirable to model real-world “is a” relationships—a giraffe is a mammal, for example. These are “semantic” relationships. Interfaces are often used to model “mechanism” relationships. A PdaItem “is not a” “comparable,” but it might well be IComparable. This interface has nothing to do with the semantic model; it’s a detail of the implementation mechanism. Explicit interface implementation is a technique for enabling the separation of mechanism concerns from model concerns. Forcing the caller to convert the object to an interface such as IComparable before treating the object as “comparable” explicitly separates out in the code when you are talking to the model and when you are dealing with its implementation mechanisms.

In general, it is preferable to limit the public surface area of a class to be “all model” with as little extraneous mechanism as possible. (Unfortunately, some mechanisms are unavoidable in .NET. You cannot get a giraffe’s hash code or convert a giraffe to a string, for example. However, you can get a Giraffe’s hash code [GetHashCode()] and convert it to a string [ToString()]. By using object as a common base class, .NET mixes model code with mechanism code, even if only to a limited extent.)

Here are several guidelines that will help you choose between an explicit implementation and an implicit implementation.

- Is the member a core part of the class functionality?
  
  Consider the ColumnValues property implementation on the Contact class. This member is not an integral part of a Contact type but rather a peripheral member probably accessed only by the ConsoleListControl class. As such, it doesn’t make sense for the

member to be immediately visible on a Contact object, cluttering up what could potentially already be a large list of members.
Alternatively, consider the IFileCompression.Compress() member. Including an implicit Compress() implementation on a ZipCompression class is a perfectly reasonable choice: Compress() is a core part of the ZipCompression class’s behavior, so it should be directly accessible from the ZipCompression class.

- Is the interface member name appropriate as a class member?
  
  Consider an ITrace interface with a member called Dump() that writes out a class’s data to a trace log. Implementing Dump() implicitly on a Person or Truck class would result in confusion as to which operation the method performs. Instead, it is preferable to implement the member explicitly so that only from a data type of ITrace, where the meaning is clearer, can the Dump() method be called. Consider using an explicit implementation if a member’s purpose is unclear on the implementing class.

- Is there already a class member with the same signature?
  
  Explicit interface member implementation does not add a named element to the type’s declaration space. Therefore, if there is already a potentially conflicting member of a type, a second one can be provided with the same name or signature as long as it is an explicit interface member.

Much of the decision making regarding implicit versus explicit interface member implementation comes down to intuition. However, these questions provide suggestions about which issues to consider when making your choice. Since changing an implementation from implicit to explicit results in a version-breaking change, it is better to err on the side of defining interfaces explicitly, allowing them to be changed to implicit implementations later on. Furthermore, since the decision between implicit and explicit does not have to be consistent across all interface members, defining some methods as explicit and others as implicit is fully supported.

## Guidelines

AVOID implementing interface members explicitly without a good reason. However, if you’re unsure, favor explicit implementation.

## Converting between the Implementing Class and Its Interfaces

Just as with a derived type and a base class, a conversion from an implementing type to its implemented interface is an implicit conversion. No cast operator is required because an instance of the implementing type will always provide all the members in the interface; therefore, the object can always be converted successfully to the interface type.

Although the conversion will always be successful from the implementing type to the implemented interface, many different types could implement a particular interface. As a consequence, you can never be certain that a “downward” cast from an interface to one of its implementing types will be successful. Therefore, converting from an interface to one of its implementing types requires an explicit cast.

## Interface Inheritance

Interfaces can derive from each other, resulting in an interface that inherits all the members in its base interfaces. As shown in Listing 7.6, the interfaces directly derived from IReadableSettingsProvider are the explicit base interfaces.

# LISTING 7.6: Deriving One Interface from Another

```
interface IReadableSettingsProvider
{
    string GetSetting(string name, string defaultValue);
}

interface ISettingsProvider : IReadableSettingsProvider
{
    void SetSetting(string name, string value);
}

class FileSettingsProvider : ISettingsProvider
{
    #region ISettingsProvider Members
    public void SetSetting(string name, string value)
    {
        // ...
    }
    #endregion
```


# Chapter 8: Interfaces

```csharp
// ...

// ERROR: Unable to call .CellValues directly
//          on a contact
values = contact.CellValues;

// First cast to IListable
values = ((IListable)contact).CellValues;

// ...
```

The cast and the call to CellValues occur within the same statement in this case. Alternatively, you could assign contact to an IListable variable before calling CellValues.
To declare an explicit interface member implementation, prefix the member name with the interface name (using Listing 8.5).

Listing 8.5: Explicit Interface Implementation

```csharp
public class Contact : PdaItem, IListable, IComparable
{
    // ...
    #region IListable Members
    string[] IListable.CellValues
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
    // ...
}
```

Listing 8.5 implements CellValues explicitly by prefixing the property name with IListable. Furthermore, since explicit interface implementations are directly associated with the interface, there is no need to modify them with virtual, override, or public. In fact, these modifiers are not allowed. The method is not treated as a public member of the class, marking it as public would be misleading.

Note that even though the override keyword is not allowed on an interface, we will still use the term "override" when referring to members that implement the interface-defined signature.

# Implicit Member Implementation

Notice that CompareTo() in Listing 8.5 does not include the IComparable prefix; it is implemented implicitly. With implicit member implementation, it is necessary only for the member to be public and for the member's signature to match the interface member's signature. Interface member implementation does not require use of the override keyword or any indication that this member is tied to the interface. Furthermore, since the member is declared just like any other class member, code that calls implicitly members can do so directly, just as it would any other class member:

```csharp
result = contact1.CompareTo(contact2);
```

In other words, implicit member implementation does not require a cast because the member is not hidden from direct invocation. Many of the modifiers disallowed on an explicit member implementation are required or optional on an implicit member implementation. For example, implicit member implementations must be public. Furthermore, virtual is optional, depending on whether derived classes may override it. Eliminating virtual will cause the member to behave as though it is sealed.

# Explicit versus Implicit Interface Implementation

The key difference between implicit and explicit member implementation lies not in the syntax of the method declaration but rather in the ability to access the method by name through an instance of the type or via the interface. When building a class, it’s desirable to model real-world “is a” relationships—a dog is a mammal, for example. These are semantic relationships. Interfaces are often used to model mechanism relationships—a “is not comparable,” but it might be. This interface has nothing to do with the semantic model; instead, it’s a detail of the implementation mechanism. Explicit interface implementation is a technique for enabling the separation of mechanism concerns from model concerns. Forcing the caller to cast the object to an interface such as IComparable before treating the object as comparable separates in the code the concepts of model and implementation implementation.

In general, it is preferable to limit the public surface area of a class to be “all model” with little mechanism as possible. Unfortunately, some mechanisms are unavoidable in .NET. In the real world, for example, you cannot get an object’s hash code or convert it to a string. However, you can get an object’s hash code [GetHashCode()] and convert to a string [ToString()] by using a common base class; .NET mixes model with mechanism, even if only to a limited extent. Here are several guidelines that will help you choose between an explicit implementation and an implicit implementation:

- Is the member core of the class functionality?
Consider the CellValues property implementation on the Contact class. This member is not an integral part of Contact type, but rather a peripheral member probably accessed only by the interface, so it doesn’t make sense for the member to be immediately visible on a Contact object, cluttering what could potentially be a large list of members. Alternatively, consider the ICompression.Compress() member. Including an implicit Compress implementation on ZipCompression class is a perfectly reasonable choice: Compress() is core part of ZipCompression class’s behavior, so it should be directly accessible from the ZipCompression class.

- Is the interface name appropriate as a class member?
Consider an ITrace interface with a member called Dump() that writes out a class’s data to a log. Implementing Dump() implicitly on Person or Truck would result in confusion as to which operation the method performs. Instead, it is preferable to implement the member explicitly so that the Dump() method can be called only from ITrace type where the meaning is clearer.

- Does a class with the same signature already exist?
Explicit interface implementation does not add a named element to the type's declaration space. Therefore, if there is already a potentially conflicting member of a type, a second one can be provided with the same name or signature as long as it is an explicit interface member.

Much of the decision-making regarding implicit explicit interface implementation comes down to intuition. However, these questions provide suggestions about issues to consider when making your choice. Since changing an implementation from implicit to explicit results in a version-breaking change, it is better to err on the side of defining interfaces explicitly, allowing them to be changed to implicit interfaces later. Furthermore, since the decision between implicit and explicit does not have to be consistent across all interface members, defining methods as explicit and others as implicit is fully supported.

# Converting between the Implementing Class and Its Interfaces

Just as with a derived type and a base class, a conversion from an implementing type to its implemented interface is an implicit conversion. No cast operator is required because an instance of the implementing type will always provide the members in the interface; therefore, the object can always be converted successfully to the interface type.

Although the conversion will always be successful from the implementing type to the implemented interface, many different types could implement a particular interface. Consequently, you can never be certain that a “downward” cast from an interface to one of its implementing types will be successful. Therefore, converting from an interface to one of its implementing types requires an explicit cast.

# Interface Inheritance

Interfaces can derive from each other, resulting in an interface that inherits all the members in its base interfaces. As shown in Listing 8.6, the interfaces directly derived from IReadOnlySettingsProvider are the base interfaces.

Listing 8.6: Deriving One Interface from Another

```csharp
interface IReadOnlySettingsProvider
{
    string GetSetting(string name, string defaultValue);
}
interface ISettingsProvider : IReadOnlySettingsProvider
{
    void SetSetting(string name, string value);
}
public class FileSettingsProvider : ISettingsProvider
{
    #region IReadOnlySettingsProvider Members
    public void SetSetting(string name, string value)
    {
        // ...
    }
    #endregion
    #region IReadOnlySettingsProvider Members
    public string GetSetting(string name, string defaultValue)
    {
        // ...
    }
    #endregion
}
```

In this case, ISettingsProvider is derived from IReadOnlySettingsProvider and therefore inherits its members. If IReadOnlySettingsProvider also had a base interface, ISettingsProvider would inherit those members as well, and the full set of...

- 6. Except C# 8.0's introduced non-private members.

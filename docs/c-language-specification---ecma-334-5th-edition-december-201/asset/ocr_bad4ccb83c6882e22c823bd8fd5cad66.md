the base interfaces of IComboBox are IControl, ITextBox, and IListBox. In other words, the IComboBox interface above inherits members SetText and SetItems as well as Paint. end example]

Members inherited from a constructed generic type are inherited after type substitution. That is, any constituent types in the member have the base class declaration’s type parameters replaced with the corresponding type arguments used in the class-base specification. [Example: In the following code

```
interface IBase<T>
{
    T[] Combine(T a, T b);
}
interface IDerived : IBase<string[,]>
{
    // Inherited: string[,] Combine(string[,] a, string[,] b);
}
```

the interface IDerived inherits the Combine method after the type parameter T is replaced with string[,]. end example]

A class or struct that implements an interface also implicitly implements all of the interface’s base interfaces.

The handling of interfaces on multiple parts of a partial interface declaration (§15.2.7) are discussed further in §15.2.4.3.

Every base interface of an interface shall be output-safe (§18.2.3.2).

# 18.3 Interface body

The interface-body of an interface defines the members of the interface.

```
interface-body:
    { interface-member-declarationsopt }
```

# 18.4 Interface members

# 18.4.1 General

The members of an interface are the members inherited from the base interfaces and the members declared by the interface itself.

```
interface-member-declarations:
    interface-member-declaration
    interface-member-declarations interface-member-declaration

interface-member-declaration:
    interface-method-declaration
    interface-property-declaration
    interface-event-declaration
    interface-indexer-declaration
```

An interface declaration declares zero or more members. The members of an interface shall be methods, properties, events, or indexers. An interface cannot contain constants, fields, operators, instance constructors, finalizers, or types, nor can an interface contain static members of any kind.

All interface members implicitly have public access. It is a compile-time error for interface member declarations to include any modifiers.

An interface-declaration creates a new declaration space (§8.3), and the type parameters and interface-member-declarations immediately contained by the interface-declaration introduce new members into this declaration space. The following rules apply to interface-member-declarations:
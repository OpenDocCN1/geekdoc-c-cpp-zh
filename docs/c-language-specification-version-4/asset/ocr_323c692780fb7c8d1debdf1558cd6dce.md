A type is *output-safe* if it is not output-unsafe, and *input-safe* if it is not input-unsafe.

# 13.1.3.2 Variance conversion

The purpose of variance annotations is to provide for more lenient (but still type safe) conversions to interface and delegate types. To this end the definitions of implicit (§6.1) and explicit conversions (§6.2) make use of the notion of variance-convertibility, which is defined as follows:

A type T<A₁, ..., Aₙ> is variance-convertible to a type T<B₁, ..., Bₙ> if T is either an interface or a delegate type declared with the variant type parameters T<X₁, ..., Xₙ>, and for each variant type parameter Xᵢ one of the following holds:

+   - Xᵢ is covariant and an implicit reference or identity conversion exists from Aᵢ to Bᵢ
+   - Xᵢ is contravariant and an implicit reference or identity conversion exists from Bᵢ to Aᵢ
+   - Xᵢ is invariant and an identity conversion exists from Aᵢ to Bᵢ

# 13.1.4 Base interfaces

An interface can inherit from zero or more interface types, which are called the *explicit base interfaces* of the interface. When an interface has one or more explicit base interfaces, then in the declaration of that interface, the interface identifier is followed by a colon and a comma separated list of base interface types.

```
interface-base:
    : interface-type-list
```

For a constructed interface type, the explicit base interfaces are formed by taking the explicit base interface declarations on the generic type declaration, and substituting, for each *type-parameter* in the base interface declaration, the corresponding *type-argument* of the constructed type.

The explicit base interfaces of an interface must be at least as accessible as the interface itself (§3.5.4). For example, it is a compile-time error to specify a *private* or *internal* interface in the *interface-base* of a *public* interface.

It is a compile-time error for an interface to directly or indirectly inherit from itself.

The *base interfaces* of an interface are the explicit base interfaces and their base interfaces. In other words, the set of base interfaces is the complete transitive closure of the explicit base interfaces, their explicit base interfaces, and so on. An interface inherits all members of its base interfaces. In the example

```
interface IControl
{
    void Paint();
}
interface ITextBox: IControl
{
    void SetText(string text);
}
interface IListBox: IControl
{
    void SetItems(string[] items);
}
interface IComboBox: ITextBox, IListBox {}
```

the base interfaces of IComboBox are IControl, ITextBox, and IListBox.

In other words, the IComboBox interface above inherits members SetText and SetItems as well as Paint.

Every base interface of an interface must be output-safe (§13.1.3.1). A class or struct that implements an interface also implicitly implements all of the interface's base interfaces.
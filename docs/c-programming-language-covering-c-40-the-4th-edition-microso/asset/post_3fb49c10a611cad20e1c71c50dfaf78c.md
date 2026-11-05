
### 13.1.3 Variant Type Parameter Lists

Variant type parameter lists can occur only on interface and delegate types. The difference from ordinary type-parameter-lists is the optional variance-annotation on each type parameter.

```
variant-type-parameter-list:
    < variant-type-parameters >

variant-type-parameters:
    attributes_opt variance-annotation_opt type-parameter
    variant-type-parameters , attributes_opt variance-annotation_opt type-parameter

variance-annotation:
    in
    out
```

If the variance annotation is out, the type parameter is said to be covariant. If the variance annotation is in, the type parameter is said to be contravariant. If there is no variance annotation, the type parameter is said to be invariant.

> ERIC LIPPERT Covariance is the property that a mapping from a type argument to a generic type preserves assignment compatibility. For example, a string may be assigned to a variable of type object. A mapping from T to IEnumerable<T> preserves the assignment compatibility; an IEnumerable<string> can be assigned to a variable of IEnumerable<object>. Thus the nomenclature that “the type parameter is covariant” is a shorthand; the thing that is actually covariant is the relationship between the type argument and the constructed type. Properly we ought to say, “The mapping from — any reference type T to IEnumerable<T> is covariant in T” but that is rather a mouthful compared to simply saying, “T is covariant,” and understanding that the longer statement is what is meant by it.

In the example

```
interface <out X, in Y, Z>
{
    X M(Y y);
    Z P { get; set; }
}
```

X is covariant, Y is contravariant, and Z is invariant.

## 13. Interfaces

### 13.1.3.1 *Variance Safety*

The occurrence of variance annotations in the type parameter list of a type restricts the places where types can occur within the type declaration.

A type T is *output-unsafe* if one of the following holds:

- T is a contravariant type parameter.
- T is an array type with an output-unsafe element type.
- T is an interface or delegate type S<A₁, ..., Aₖ> constructed from a generic type S<X₁, ..., Xₖ> where for at least one Aᵢ one of the following holds:
  - Xᵢ is covariant or invariant and Aᵢ is output-unsafe.
  - Xᵢ is contravariant or invariant and Aᵢ is input-safe.

A type T is *input-unsafe* if one of the following holds:

- T is a covariant type parameter.
- T is an array type with an input-unsafe element type.
- T is an interface or delegate type S<A₁, ..., Aₖ> constructed from a generic type S<X₁, ..., Xₖ> where for at least one Aᵢ one of the following holds:
  - Xᵢ is covariant or invariant and Aᵢ is input-unsafe.
  - Xᵢ is contravariant or invariant and Aᵢ is output-unsafe.

Intuitively, an output-unsafe type is prohibited in an output position, and an input-unsafe type is prohibited in an input position.

A type is *output-safe* if it is not output-unsafe, and *input-safe* if it is not input-unsafe.

### 13.1.3.2 *Variance Conversion*

The purpose of variance annotations is to provide for more lenient (but still type-safe) conversions to interface and delegate types. To this end, the definitions of implicit (§6.1) and explicit conversions (§6.2) make use of the notion of variance convertibility, which is defined as follows:

A type T<A₁, ..., Aₙ> is variance convertible to a type T<B₁, ..., Bₙ> if T is either an interface or a delegate type declared with variant type parameters T<X₁, ..., Xₙ>, and for each variant type parameter Xᵢ one of the following holds:

- Xᵢ is covariant and an implicit reference or identity conversion exists from Aᵢ to Bᵢ.
- Xᵢ is contravariant and an implicit reference or identity conversion exists from Bᵢ to Aᵢ.
- Xᵢ is invariant and an identity conversion exists from Aᵢ to Bᵢ.

> **JON SKEET** I suspect many developers will never need to declare their own variant interfaces or delegates. In fact, my guess is that a lot of the time we won’t even notice when we’re *using* variance—it will just mean code that we would intuitively expect to work will now do so, even though it would have failed to compile in C# 3.0.

### 13.1.4 Base Interfaces

An interface can inherit from zero or more interface types, which are called the *explicit base interfaces* of the interface. When an interface has one or more explicit base interfaces, then in the declaration of that interface, the interface identifier is followed by a colon and a comma-separated list of base interface types.

```
interface-base:
    : interface-type-list
```

For a constructed interface type, the explicit base interfaces are formed by taking the explicit base interface declarations on the generic type declaration, and substituting, for each *type-parameter* in the base interface declaration, the corresponding *type-argument* of the constructed type.

The explicit base interfaces of an interface must be at least as accessible as the interface itself (§3.5.4). For example, it is a compile-time error to specify a *private* or *internal* interface in the *interface-base* of a *public* interface.

It is a compile-time error for an interface to directly or indirectly inherit from itself.

> **VLADIMIR RESHETNIKOV** For the purposes of this rule, type arguments (if any) are ignored. For instance, although `I<T>` and `I<I<T>>` are different types, the following declaration is still invalid:
> 
> ```csharp
> interface I<T> : I<I<T>> { }
> ```
> 
> Conversely, it is perfectly valid for an interface to appear within a type argument for its base interface:
> 
> ```csharp
> interface IA<T> { }
> interface IB : IA<I[]> { }  // Okay
> ```

The *base interfaces* of an interface are the explicit base interfaces and their base interfaces. In other words, the set of base interfaces is the complete transitive closure of the explicit base interfaces, their explicit base interfaces, and so on. An interface inherits all members of its base interfaces. In the example

```
interface IControl
{
    void Paint();
}

interface ITextBox : IControl
{
    void SetText(string text);
}

interface IListBox : IControl
{
    void SetItems(string[] items);
}

interface IComboBox : ITextBox, IListBox { }
```

the base interfaces of IComboBox are IControl, ITextBox, and IListBox.

In other words, the IComboBox interface above inherits members SetText and SetItems as well as Paint.

Every base interface of an interface must be output-safe (§13.1.3.1). A class or struct that implements an interface also implicitly implements all of the interface's base interfaces.

> **ERIC LIPPERT**  “Inheritance” is an unfortunate choice of words for interfaces. One normally thinks of inheritance from a base as sharing implementation, which interfaces plainly do not do. I prefer to think of interfaces as contracts that may specify other contracts that must also be fulfilled, rather than as contracts that “inherit” other contracts.

> **JESSE LIBERTY**  A naming convention has arisen of prefixing all interfaces with the letter “I” (IControl, IWriteable, IClaudius). There is no compelling reason to do so, yet it has persisted for at least a decade as a last remnant of “Hungarian” notation. Removing the “I”, in the end, makes for more readable code.

### 13.1.5 Interface Body

The interface-body of an interface defines the members of the interface.

```
interface-body:
{ interface-member-declarations_opt }
```

### 13.2 Interface Members

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

An interface declaration may declare zero or more members. The members of an interface must be methods, properties, events, or indexers. An interface cannot contain constants, fields, operators, instance constructors, destructors, or types, nor can an interface contain static members of any kind.

All interface members implicitly have public access. It is a compile-time error for interface member declarations to include any modifiers. In particular, interface members cannot be declared with the modifiers abstract, public, protected, internal, private, virtual, override, or static.

> **JON SKEET** It would occasionally be nice to be able to create an internal interface with internal members that could be implemented implicitly by internal methods. Currently an internal interface forces implementing types either to expose public methods or to use explicit interface implementation; in some cases, neither of these choices is particularly pleasant.

The example

```
public delegate void StringListEvent(IStringList sender);

public interface IStringList
{
    void Add(string s);
    int Count { get; }
    event StringListEvent Changed;
    string this[int index] { get; set; }
}
```

declares an interface that contains one each of the possible kinds of members: a method, a property, an event, and an indexer.


Hiding an inherited member is not considered an error, but it does cause the compiler to issue a warning. To suppress the warning, the declaration of the derived interface member shall include a new modifier to indicate that the derived member is intended to hide the base member. This topic is discussed further in §7.7.2.3.

If a new modifier is included in a declaration that doesn't hide an inherited member, a warning is issued to that effect. This warning is suppressed by removing the new modifier.

> Note: The members in class object are not, strictly speaking, members of any interface (§17.4). However, the members in class object are available via member lookup in any interface type (§11.5). end note

The set of members of an interface declared in multiple parts (§14.2.7) is the union of the members declared in each part. The bodies of all parts of the interface declaration share the same declaration space (§7.3), and the scope of each member (§7.7) extends to the bodies of all the parts.

## 17.4.2 Interface methods

Interface methods are declared using interface_method_declarations:

```
interface_method_declaration
: attributes? 'new'? return_type identifier type_parameter_list?
'(' formal_parameter_list? ')' type_parameter_constraints_clause* ';'
;
```

The attributes, return_type, identifier, and formal_parameter_list of an interface method declaration have the same meaning as those of a method declaration in a class (§14.6). An interface method declaration is not permitted to specify a method body, and the declaration therefore always ends with a semicolon. An interface_method_declaration shall not have type_parameter_constraints_clauses unless it also has a type_parameter_list.

All formal parameter types of an interface method shall be input-safe (§17.2.3.2), and the return type shall be either void or output-safe. In addition, any output or reference formal parameter types shall also be output-safe.

> Note: Output parameters are required to be input-safe due to common implementation restrictions. end note

Furthermore, each class type constraint, interface type constraint and type parameter constraint on any type parameters of the method shall be input-safe.

Furthermore, each class type constraint, interface type constraint and type parameter constraint on any type parameter of the method shall be input-safe.

These rules ensure that any covariant or contravariant usage of the interface remains typesafe.

Example:

```
interface I<out T>
{
    void M<U>() where U : T;
}
```

is ill-formed because the usage of T as a type parameter constraint on U is not input-safe.

Were this restriction not in place it would be possible to violate type safety in the following manner:

```
class B {}
class D : B {}
class E : B {}
class C : I<D>
{
    public void M<U>() {...}
}
```

```
...
I<B> b = new C();
b.M<E>();
```

This is actually a call to C.M<E>. But that call requires that E derive from D, so type safety would be violated here.

*end example*

## 17.4.3 Interface properties

Interface properties are declared using *interface_property_declarations*:

```
interface_property_declaration
    : attributes? 'new'? type identifier '{' interface_accessors '}'
    ;

interface_accessors
    : attributes? 'get' ';'
    | attributes? 'set' ';'
    | attributes? 'get' ';' attributes? 'set' ';'
    | attributes? 'set' ';' attributes? 'get' ';'
    ;
```

The *attributes*, *type*, and *identifier* of an interface property declaration have the same meaning as those of a property declaration in a class (§14.7).

The accessors of an interface property declaration correspond to the accessors of a class property declaration (§14.7.3), except that the accessor body shall always be a semicolon. Thus, the accessors simply indicate whether the property is read-write, read-only, or write-only.

The type of an interface property shall be output-safe if there is a get accessor, and shall be input-safe if there is a set accessor.

## 17.4.4 Interface events

Interface events are declared using *interface_event_declarations*:

```
interface_event_declaration
    : attributes? 'new'? 'event' type identifier ';'
    ;
```

The *attributes*, *type*, and *identifier* of an interface event declaration have the same meaning as those of an event declaration in a class (§14.8).

The type of an interface event shall be input-safe.

## 17.4.5 Interface indexers

Interface indexers are declared using *interface_indexer_declarations*:

```
interface_indexer_declaration:
    attributes? 'new'? type 'this' '[' formal_parameter_list ']' '{'
```

The first two statements cause compile-time errors because the member lookup (§11.5) of Count in IListCounter is ambiguous. As illustrated by the example, the ambiguity is resolved by casting x to the appropriate base interface type. Such casts have no run-time costs—they merely consist of viewing the instance as a less derived type at compile-time.

end example

Example: In the following code

```
interface IInteger
{
    void Add(int i);
}

interface IDouble
{
    void Add(double d);
}

interface INumber : IInteger, IDouble {}

class C
{
    void Test(INumber n)
    {
        n.Add(1);        // Invokes IInteger.Add
        n.Add(1.0);      // Only IDouble.Add is applicable
        ((IInteger)n).Add(1); // Only IInteger.Add is a candidate
        ((IDouble)n).Add(1);  // Only IDouble.Add is a candidate
    }
}
```

the invocation n.Add(1) selects IInteger.Add by applying overload resolution rules of §11.6.4. Similarly, the invocation n.Add(1.0) selects IDouble.Add. When explicit casts are inserted, there is only one candidate method, and thus no ambiguity.

end example

Example: In the following code

```
interface IBase
{
    void F(int i);
}

interface ILeft : IBase
{
    new void F(int i);
}

interface IRight : IBase
{
    void G();
}

interface IDerived : ILeft, IRight {}
```

```
class A
{
    void Test(IDerived d)
    {
        d.F(1); // Invokes ILeft.F
        ((IBase)d).F(1); // Invokes IBase.F
        ((ILeft)d).F(1); // Invokes ILeft.F
        ((IRight)d).F(1); // Invokes IBase.F
    }
}
```

the IBase.F member is hidden by the ILeft.F member. The invocation d.F(1) thus selects ILeft.F, even though IBase.F appears to not be hidden in the access path that leads through IRight.

The intuitive rule for hiding in multiple-inheritance interfaces is simply this: If a member is hidden in any access path, it is hidden in all access paths. Because the access path from IDerived to ILeft to IBase hides IBase.F, the member is also hidden in the access path from IDerived to IRight to IBase.

*end example*

## 17.5 Qualified interface member names

An interface member is sometimes referred to by its qualified interface member name. The qualified name of an interface member consists of the name of the interface in which the member is declared, followed by a dot, followed by the name of the member. The qualified name of a member references the interface in which the member is declared.

*Example: Given the declarations*

```
interface IControl
{
    void Paint();
}
interface ITextBox : IControl
{
    void SetText(string text);
}
```

the qualified name of Paint is IControl.Paint and the qualified name of SetText is ITextBox.SetText. In the example above, it is not possible to refer to Paint as ITextBox.Paint.

*end example*

When an interface is part of a namespace, a qualified interface member name can include the namespace name.

*Example:*

```
namespace System
{
    public interface ICloneable
    {
        object Clone();
    }
}
```

Within the System namespace, both ICloneable.Clone and System.ICloneable.Clone are qualified interface member names for the Clone method.

end example

## 17.6 Interface implementations

### 17.6.1 General

Interfaces may be implemented by classes and structs. To indicate that a class or struct directly implements an interface, the interface is included in the base class list of the class or struct.

Example:

```
interface ICloneable
{
    object Clone();
}
interface IComparable
{
    int CompareTo(object other);
}
class ListEntry : ICloneable, IComparable
{
    public object Clone() {...}
    public int CompareTo(object other) {...}
}
```

end example

A class or struct that directly implements an interface also implicitly implements all of the interface's base interfaces. This is true even if the class or struct doesn't explicitly list all base interfaces in the base class list.

Example:

```
interface IControl
{
    void Paint();
}
interface ITextBox : IControl
{
    void SetText(string text);
}
class TextBox : ITextBox
{
    public void Paint() {...}
    public void SetText(string text) {...}
}
```

Here, class TextBox implements both IControl and ITextBox.

end example

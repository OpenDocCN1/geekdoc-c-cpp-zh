
The explicit base interfaces of an interface shall be at least as accessible as the interface itself (§7.5.5).

Note: For example, it is a compile-time error to specify a private or internal interface in the interface_base of a public interface. end note

It is a compile-time error for an interface to directly or indirectly inherit from itself.

The base interfaces of an interface are the explicit base interfaces and their base interfaces. In other words, the set of base interfaces is the complete transitive closure of the explicit base interfaces, their explicit base interfaces, and so on. An interface inherits all members of its base interfaces.

Example: In the following code

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

interface IComboBox: ITextBox, IListBox {}
```

the base interfaces of IComboBox are IControl, ITextBox, and IListBox. In other words, the IComboBox interface above inherits members SetText and SetItems as well as Paint.

end example

Members inherited from a constructed generic type are inherited after type substitution. That is, any constituent types in the member have the base interface declaration's type parameters replaced with the corresponding type arguments used in the interface_base specification.

Example: In the following code

```
interface IBase<T>
{
    T[] Combine(T a, T b);
}

interface IDerived : IBase<string[,]>
{
    // Inherited: string[,][,] Combine(string[,] a, string[,] b);
}
```

the interface IDerived inherits the Combine method after the type parameter T is replaced with string[,].

end example

A class or struct that implements an interface also implicitly implements all of the interface's base interfaces.

The handling of interfaces on multiple parts of a partial interface declaration (§15.2.7) is discussed further in §15.2.4.3.

Every base interface of an interface shall be output-safe (§18.2.3.2).

## 18.3 接口体

The interface_body of an interface defines the members of the interface.

```
interface_body
  : '{' interface_member_declaration* '}'
  ;
```

## 18.4 接口成员

### 18.4.1 通用

The members of an interface are the members inherited from the base interfaces and the members declared by the interface itself.

```
interface_member_declaration
  : interface_method_declaration
  | interface_property_declaration
  | interface_event_declaration
  | interface_indexer_declaration
  ;
```

An interface declaration declares zero or more members. The members of an interface shall be methods, properties, events, or indexers. An interface cannot contain constants, fields, operators, instance constructors, finalizers, or types, nor can an interface contain static members of any kind.

All interface members implicitly have public access. It is a compile-time error for interface member declarations to include any modifiers.

An interface_declaration creates a new declaration space (§7.3), and the type parameters and interface_member_declarations immediately contained by the interface_declaration introduce new members into this declaration space. The following rules apply to interface_member_declarations:

- The name of a type parameter in the type_parameter_list of an interface declaration shall differ from the names of all other type parameters in the same type_parameter_list and shall differ from the names of all members of the interface.
- The name of a method shall differ from the names of all properties and events declared in the same interface. In addition, the signature (§7.6) of a method shall differ from the signatures of all other methods declared in the same interface, and two methods declared in the same interface may not have signatures that differ solely by in, out, and ref.
- The name of a property or event shall differ from the names of all other members declared in the same interface.
- The signature of an indexer shall differ from the signatures of all other indexers declared in the same interface.

The inherited members of an interface are specifically not part of the declaration space of the interface. Thus, an interface is allowed to declare a member with the same name or signature as an inherited member. When this occurs, the derived interface member is said to hide the base interface member.

Hiding an inherited member is not considered an error, but it does cause the compiler to issue a warning. To suppress the warning, the declaration of the derived interface member shall include a new modifier to indicate that the derived member is intended to hide the base member. This topic is discussed further in §7.7.2.3.

If a new modifier is included in a declaration that doesn't hide an inherited member, a warning is issued to that effect. This warning is suppressed by removing the new modifier.

> Note: The members in class object are not, strictly speaking, members of any interface (§18.4). However, the members in class object are available via member lookup in any interface type (§12.5). end note

The set of members of an interface declared in multiple parts (§15.2.7) is the union of the members declared in each part. The bodies of all parts of the interface declaration share the same declaration space (§7.3), and the scope of each member (§7.7) extends to the bodies of all the parts.

### 18.4.2 接口方法

Interface methods are declared using interface_method_declarations:

```
interface_method_declaration
  : attributes? 'new'? return_type interface_method_header
  | attributes? 'new'? ref_kind ref_return_type interface_method_header
  ;

interface_method_header
  : identifier '(' formal_parameter_list? ')' ';'
  | identifier type_parameter_list '(' formal_parameter_list? ')'
    type_parameter_constraints_clause* ';'
  ;
```

The attributes, return_type, ref_return_type, identifier, and formal_parameter_list of an interface method declaration have the same meaning as those of a method declaration in a class (§15.6). An interface method declaration is not permitted to specify a method body, and the declaration therefore always ends with a semicolon.

All formal parameter types of an interface method shall be input-safe (§18.2.3.2), and the return type shall be either void or output-safe. In addition, any output or reference formal parameter types shall also be output-safe.

> Note: Output parameters are required to be input-safe due to common implementation restrictions. end note

Furthermore, each class type constraint, interface type constraint and type parameter constraint on any type parameters of the method shall be input-safe. Furthermore, each class type constraint, interface type constraint and type parameter constraint on any type parameter of the method shall be input-safe.

These rules ensure that any covariant or contravariant usage of the interface remains typesafe.

Example:

```
interface I<out T>
{
    void M<U>() where U : T;    // Error
}
```

is ill-formed because the usage of T as a type parameter constraint on U is not input-safe.

Were this restriction not in place it would be possible to violate type safety in the following manner:

```csharp
class B {}
class D : B {}
class E : B {}
class C : I<D>
{
    public void M<U>() {...}
}

...

I<B> b = new C();
b.M<E>();
```

This is actually a call to C.M<E>. But that call requires that E derive from D, so type safety would be violated here.

end example

### 18.4.3 接口属性

Interface properties are declared using interface_property_declarations:

```
interface_property_declaration
    : attributes? 'new'? type identifier '{' interface_accessors '}'
    | attributes? 'new'? ref_kind type identifier '{' ref_interface_accessor '}'
    ;

interface_accessors
    : attributes? 'get' ';'
    | attributes? 'set' ';'
    | attributes? 'get' ';' attributes? 'set' ';'
    | attributes? 'set' ';' attributes? 'get' ';'
    ;

ref_interface_accessor
    : attributes? 'get' ';'
    ;
```

The *attributes*, *type*, and *identifier* of an interface property declaration have the same meaning as those of a property declaration in a class (§15.7).

The accessors of an interface property declaration correspond to the accessors of a class property declaration (§15.7.3), except that the *accessor_body* shall always be a semicolon. Thus, the accessors simply indicate whether the property is read-write, read-only, or write-only.

The type of an interface property shall be output-safe if there is a get accessor, and shall be input-safe if there is a set accessor.

### 18.4.4 接口事件

Interface events are declared using *interface_event_declarations*:

```
interface_event_declaration
    : attributes? 'new'? 'event' type identifier ';'
    ;
```

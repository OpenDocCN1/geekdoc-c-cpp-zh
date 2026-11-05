
```
for (int i = 0; i < 10; i++)
{
    H();
}
}
```

end note

## 7.4 Members

### 7.4.1 General

Namespaces and types have members.

> Note: The members of an entity are generally available through the use of a qualified name that starts with a reference to the entity, followed by a "." token, followed by the name of the member.
> end note

Members of a type are either declared in the type declaration or inherited from the base class of the type. When a type inherits from a base class, all members of the base class, except instance constructors, finalizers, and static constructors become members of the derived type. The declared accessibility of a base class member does not control whether the member is inherited—inheritance extends to any member that isn't an instance constructor, static constructor, or finalizer.

> Note: However, an inherited member might not be accessible in a derived type, for example because of its declared accessibility (§7.5.2). end note

### 7.4.2 Namespace members

Namespaces and types that have no enclosing namespace are members of the global namespace. This corresponds directly to the names declared in the global declaration space.

Namespaces and types declared within a namespace are members of that namespace. This corresponds directly to the names declared in the declaration space of the namespace.

Namespaces have no access restrictions. It is not possible to declare private, protected, or internal namespaces, and namespace names are always publicly accessible.

### 7.4.3 Struct members

The members of a struct are the members declared in the struct and the members inherited from the struct's direct base class System.ValueType and the indirect base class object.

The members of a simple type correspond directly to the members of the struct type aliased by the simple type (§8.3.5).

### 7.4.4 Enumeration members

The members of an enumeration are the constants declared in the enumeration and the members inherited from the enumeration's direct base class System.Enum and the indirect base classes System.ValueType and object.

### 7.4.5 Class members

The members of a class are the members declared in the class and the members inherited from the base class (except for class object which has no base class). The members inherited from the base class include the constants, fields, methods, properties, events, indexers, operators, and types of the base class, but not the instance constructors, finalizers, and static constructors of the base class. Base class members are inherited without regard to their accessibility.

A class declaration may contain declarations of constants, fields, methods, properties, events, indexers, operators, instance constructors, finalizers, static constructors, and types.

The members of object (§8.2.3) and string (§8.2.5) correspond directly to the members of the class types they alias.

### 7.4.6 Interface members

The members of an interface are the members declared in the interface and in all base interfaces of the interface.

Note: The members in class object are not, strictly speaking, members of any interface (§17.4). However, the members in class object are available via member lookup in any interface type (§11.5). end note

### 7.4.7 Array members

The members of an array are the members inherited from class System.Array.

### 7.4.8 Delegate members

A delegate inherits members from class System.Delegate. Additionally, it contains a method named Invoke with the same return type and formal parameter list specified in its declaration (§19.2). An invocation of this method shall behave identically to a delegate invocation (§19.6) on the same delegate instance.

An implementation may provide additional members, either through inheritance or directly in the delegate itself.

## 7.5 Member access

### 7.5.1 General

Declarations of members allow control over member access. The accessibility of a member is established by the declared accessibility (§7.5.2) of the member combined with the accessibility of the immediately containing type, if any.

When access to a particular member is allowed, the member is said to be accessible. Conversely, when access to a particular member is disallowed, the member is said to be inaccessible. Access to a member is permitted when the textual location in which the access takes place is included in the accessibility domain (§7.5.3) of the member.

### 7.5.2 Declared accessibility

The declared accessibility of a member can be one of the following:

- Public, which is selected by including a public modifier in the member declaration. The intuitive meaning of public is "access not limited".
- Protected, which is selected by including a *protected* modifier in the member declaration. The intuitive meaning of *protected* is “access limited to the containing class or types derived from the containing class”.
- Internal, which is selected by including an *internal* modifier in the member declaration. The intuitive meaning of *internal* is “access limited to this assembly”.
- Protected internal, which is selected by including both a *protected* and an *internal* modifier in the member declaration. The intuitive meaning of *protected internal* is “accessible within this assembly as well as types derived from the containing class”.
- Private, which is selected by including a *private* modifier in the member declaration. The intuitive meaning of *private* is “access limited to the containing type”.

Depending on the context in which a member declaration takes place, only certain types of declared accessibility are permitted. Furthermore, when a member declaration does not include any access modifiers, the context in which the declaration takes place determines the default declared accessibility.

- Namespaces implicitly have *public* declared accessibility. No access modifiers are allowed on namespace declarations.
- Types declared directly in compilation units or namespaces (as opposed to within other types) can have *public* or *internal* declared accessibility and default to *internal* declared accessibility.
- Class members can have any of the five kinds of declared accessibility and default to *private* declared accessibility.
  *Note:* A type declared as a member of a class can have any of the five kinds of declared accessibility, whereas a type declared as a member of a namespace can have only *public* or *internal* declared accessibility. *end note*
- Struct members can have *public*, *internal*, or *private* declared accessibility and default to *private* declared accessibility because structs are implicitly sealed. Struct members introduced in a struct (that is, not inherited by that struct) cannot have *protected* or *protected internal* declared accessibility.
  *Note:* A type declared as a member of a struct can have *public*, *internal*, or *private* declared accessibility, whereas a type declared as a member of a namespace can have only *public* or *internal* declared accessibility. *end note*
- Interface members implicitly have *public* declared accessibility. No access modifiers are allowed on interface member declarations.
- Enumeration members implicitly have *public* declared accessibility. No access modifiers are allowed on enumeration member declarations.

### 7.5.3 Accessibility domains

The *accessibility domain* of a member consists of the (possibly disjoint) sections of program text in which access to the member is permitted. For purposes of defining the accessibility domain of a member, a member is said to be *top-level* if it is not declared within a type, and a member is said to be *nested* if it is declared within another type. Furthermore, the *program text* of a program is defined as all text contained in all compilation units of the program, and the program text of a type is defined as all text contained in the *type declarations* of that type (including, possibly, types that are nested within the type).

The accessibility domain of a predefined type (such as `object`, `int`, or `double`) is unlimited.

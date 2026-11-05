
## 3.4 Members

Namespaces and types have members. The members of an entity are generally available through the use of a qualified name that starts with a reference to the entity, followed by a “.” token, followed by the name of the member.

Members of a type are either declared in a type declaration or inherited from the base class of the type. When a type inherits from a base class, all members of the base class, except instance constructors, destructors, and static constructors, become members of the derived type. The declared accessibility of a base class member does not control whether the member is inherited—inheritance extends to any member that isn’t an instance constructor, static constructor, or destructor. However, an inherited member may not be accessible in a derived type, either because of its declared accessibility (§3.5.1) or because it is hidden by a declaration in the type itself (§3.7.1.2).

### 3.4.1 Namespace Members

Namespaces and types that have no enclosing namespace are members of the global namespace. This corresponds directly to the names declared in the global declaration space.

Namespaces and types declared within a namespace are members of that namespace. This corresponds directly to the names declared in the declaration space of the namespace.

Namespaces have no access restrictions. It is not possible to declare private, protected, or internal namespaces, and namespace names are always publicly accessible.

### 3.4.2 Struct Members

The members of a struct are the members declared in the struct and the members inherited from the struct’s direct base class System.ValueType and the indirect base class object.

The members of a simple type correspond directly to the members of the struct type aliased by the simple type:

- The members of sbyte are the members of the System.SByte struct.
- The members of byte are the members of the System.Byte struct.
- The members of short are the members of the System.Int16 struct.
- The members of ushort are the members of the System.UInt16 struct.
- The members of int are the members of the System.Int32 struct.
- The members of uint are the members of the System.UInt32 struct.
- The members of long are the members of the System.Int64 struct.
- The members of `ulong` are the members of the System.UInt64 struct.
- The members of `char` are the members of the System.Char struct.
- The members of `float` are the members of the System.Single struct.
- The members of `double` are the members of the System.Double struct.
- The members of `decimal` are the members of the System.Decimal struct.
- The members of `bool` are the members of the System.Boolean struct.

### 3.4.3 Enumeration Members

The members of an enumeration are the constants declared in the enumeration and the members inherited from the enumeration's direct base class System.Enum and the indirect base classes System.ValueType and object.

### 3.4.4 Class Members

The members of a class are the members declared in the class and the members inherited from the base class (except for class object, which has no base class). The members inherited from the base class include the constants, fields, methods, properties, events, indexers, operators, and types of the base class, but not the instance constructors, destructors, and static constructors of the base class. Base class members are inherited without regard to their accessibility.

A class declaration may contain declarations of constants, fields, methods, properties, events, indexers, operators, instance constructors, destructors, static constructors, and types.

The members of object and string correspond directly to the members of the class types they alias:

- The members of `object` are the members of the System.Object class.
- The members of `string` are the members of the System.String class.

### 3.4.5 Interface Members

The members of an interface are the members declared in the interface and in all base interfaces of the interface. The members in class object are not, strictly speaking, members of any interface (§13.2). However, the members in class object are available via member lookup in any interface type (§7.4).

### 3.4.6 Array Members

The members of an array are the members inherited from class System.Array.

### 3.4.7 Delegate Members

The members of a delegate are the members inherited from class System.Delegate.

> VLADIMIR RESHETNIKOV In the Microsoft implementation of C#, the members of a delegate also include the instance methods Invoke, BeginInvoke, and EndInvoke, and the members inherited from class System.MulticastDelegate.

> JON SKEET The Invoke, BeginInvoke, and EndInvoke methods mentioned by Vladimir cannot be specified within the Delegate or MulticastDelegate types, as they depend on the parameters and return type of the delegate. This is an example of parameterized typing that generics couldn’t quite handle even if it had been present from the first version of C#.

## 3.5 Member Access

Declarations of members allow control over member access. The accessibility of a member is established by the declared accessibility (§3.5.1) of the member combined with the accessibility of the immediately containing type, if any.

When access to a particular member is allowed, the member is said to be accessible. Conversely, when access to a particular member is disallowed, the member is said to be inaccessible. Access to a member is permitted when the textual location in which the access takes place is included in the accessibility domain (§3.5.2) of the member.

### 3.5.1 Declared Accessibility

The declared accessibility of a member can be one of the following:

- Public, which is selected by including a public modifier in the member declaration. The intuitive meaning of public is “access not limited.”
- Protected, which is selected by including a protected modifier in the member declaration. The intuitive meaning of protected is “access limited to the containing class or types derived from the containing class.”
- Internal, which is selected by including an internal modifier in the member declaration. The intuitive meaning of internal is “access limited to this program.”
- Protected internal (meaning protected or internal), which is selected by including both a protected and an internal modifier in the member declaration. The intuitive meaning of protected internal is "access limited to this program or types derived from the containing class."
- Private, which is selected by including a private modifier in the member declaration. The intuitive meaning of private is "access limited to the containing type."

> > **JESSE LIBERTY** While there is always a default accessibility, it is good programming practice to declare the accessibility explicitly. This makes for code that is easier to read and far easier to maintain.

> > **JON SKEET** The default accessibility is nicely chosen in C#: It's always the most restrictive level available, with the exception of making a property getter/setter more restrictive than the overall property declaration. I used to prefer to leave the accessibility as an implicit value, but I've come around to Jesse's point of view over time. Making anything explicit indicates that you are aware that a choice exists, and that you have deliberately chosen this particular option. If you leave the choice implicit, it could be because you wanted that option—or it could be because you forgot there was a choice to make in the first place.

Depending on the context in which a member declaration takes place, only certain types of declared accessibility are permitted. Furthermore, when a member declaration does not include any access modifiers, the context in which the declaration takes place determines the default declared accessibility.

- Namespaces implicitly have public declared accessibility. No access modifiers are allowed on namespace declarations.
- Types declared in compilation units or namespaces can have public or internal declared accessibility and default to internal declared accessibility.
- Class members can have any of the five kinds of declared accessibility and default to private declared accessibility. (Note that a type declared as a member of a class can have any of the five kinds of declared accessibility, whereas a type declared as a member of a namespace can have only public or internal declared accessibility.)

> > **VLADIMIR RESHETNIKOV** If a sealed class declares a protected or protected internal member, a warning is issued. If a static class declares a protected or protected internal member, a compile-time error occurs (CS1057).

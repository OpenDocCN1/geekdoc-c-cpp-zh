# 7.4.5 Class members

The members of a class are the members declared in the class and the members inherited from the base class (except for class object which has no base class). The members inherited from the base class include the constants, fields, methods, properties, events, indexers, operators, and types of the base class, but not the instance constructors, finalizers, and static constructors of the base class. Base class members are inherited without regard to their accessibility.

A class declaration may contain declarations of constants, fields, methods, properties, events, indexers, operators, instance constructors, finalizers, static constructors, and types.

The members of object (§8.2.3) and string (§8.2.5) correspond directly to the members of the class types they alias.

# 7.4.6 Interface members

The members of an interface are the members declared in the interface and in all base interfaces of the interface.

Note: The members in class object are not, strictly speaking, members of any interface (§17.4). However, the members in class object are available via member lookup in any interface type (§11.5). end note

# 7.4.7 Array members

The members of an array are the members inherited from class System.Array.

# 7.4.8 Delegate members

A delegate inherits members from class System.Delegate. Additionally, it contains a method named Invoke with the same return type and formal parameter list specified in its declaration (§19.2). An invocation of this method shall behave identically to a delegate invocation (§19.6) on the same delegate instance.

An implementation may provide additional members, either through inheritance or directly in the delegate itself.

# 7.5 Member access

# 7.5.1 General

Declarations of members allow control over member access. The accessibility of a member is established by the declared accessibility (§7.5.2) of the member combined with the accessibility of the immediately containing type, if any.

When access to a particular member is allowed, the member is said to be accessible. Conversely, when access to a particular member is disallowed, the member is said to be inaccessible. Access to a member is permitted when the textual location in which the access takes place is included in the accessibility domain (§7.5.3) of the member.

# 7.5.2 Declared accessibility

The declared accessibility of a member can be one of the following:

+   - Public, which is selected by including a public modifier in the member declaration. The intuitive meaning of public is "access not limited".
# 3.4.5 Interface members

The members of an interface are the members declared in the interface and in all base interfaces of the interface. The members in class object are not, strictly speaking, members of any interface (§13.2). However, the members in class object are available via member lookup in any interface type (§7.4).

# 3.4.6 Array members

The members of an array are the members inherited from class System.Array.

# 3.4.7 Delegate members

The members of a delegate are the members inherited from class System.Delegate.

# 3.5 Member access

Declarations of members allow control over member access. The accessibility of a member is established by the declared accessibility (§3.5.1) of the member combined with the accessibility of the immediately containing type, if any.

When access to a particular member is allowed, the member is said to be accessible. Conversely, when access to a particular member is disallowed, the member is said to be inaccessible. Access to a member is permitted when the textual location in which the access takes place is included in the accessibility domain (§3.5.2) of the member.

# 3.5.1 Declared accessibility

The declared accessibility of a member can be one of the following:

+   - Public, which is selected by including a `public` modifier in the member declaration. The intuitive meaning of `public` is "access not limited".
+   - Protected, which is selected by including a `protected` modifier in the member declaration. The intuitive meaning of `protected` is "access limited to the containing class or types derived from the containing class".
+   - Internal, which is selected by including an `internal` modifier in the member declaration. The intuitive meaning of `internal` is "access limited to this program".
+   - Protected internal (meaning protected or internal), which is selected by including both a `protected` and an `internal` modifier in the member declaration. The intuitive meaning of `protected internal` is "access limited to this program or types derived from the containing class".
+   - Private, which is selected by including a `private` modifier in the member declaration. The intuitive meaning of `private` is "access limited to the containing type".

Depending on the context in which a member declaration takes place, only certain types of declared accessibility are permitted. Furthermore, when a member declaration does not include any access modifiers, the context in which the declaration takes place determines the default declared accessibility.

+   - Namespaces implicitly have `public` declared accessibility. No access modifiers are allowed on namespace declarations.
+   - Types declared in compilation units or namespaces can have `public` or `internal` declared accessibility and default to `internal` declared accessibility.
+   - Class members can have any of the five kinds of declared accessibility and default to `private` declared accessibility. (Note that a type declared as a member of a class can have any of the five kinds of declared accessibility, whereas a type declared as a member of a namespace can have only `public` or `internal` declared accessibility.)
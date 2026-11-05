In the example above, the declaration of F in Derived hides the F that was inherited from Base, but since the new F in Derived has private access, its scope does not extend to MoreDerived. Thus, the call F() in MoreDerived.G is valid and will invoke Base.F.

*end example*

# 7.8 Namespace and type names

# 7.8.1 General

Several contexts in a C# program require a namespace_name or a type_name to be specified.

```
namespace_name
  : namespace_or_type_name
  ;

type_name
  : namespace_or_type_name
  ;

namespace_or_type_name
  : identifier type_argument_list?
  | namespace_or_type_name '.' identifier type_argument_list?
  | qualified_alias_member
  ;
```

A namespace_name is a namespace_or_type_name that refers to a namespace.

Following resolution as described below, the namespace_or_type_name of a namespace_name shall refer to a namespace, or otherwise a compile-time error occurs. No type arguments (§8.4.2) can be present in a namespace_name (only types can have type arguments).

A type_name is a namespace_or_type_name that refers to a type. Following resolution as described below, the namespace_or_type_name of a type_name shall refer to a type, or otherwise a compile-time error occurs.

If the namespace_or_type_name is a qualified_alias_member its meaning is as described in §14.8.1. Otherwise, a namespace_or_type_name has one of four forms:

+   - `I`
+   - `I<A₁, ..., Aₓ>`
+   - `N.I`
+   - `N.I<A₁, ..., Aₓ>`

where I is a single identifier, N is a namespace_or_type_name and <A₁, ..., Aₓ> is an optional type_argument_list. When no type_argument_list is specified, consider x to be zero.

The meaning of a namespace_or_type_name is determined as follows:

+   - If the namespace_or_type_name is a qualified_alias_member, the meaning is as specified in §14.8.1.
+   - Otherwise, if the namespace_or_type_name is of the form I or of the form I<A₁, ..., Aₓ>:
+     - If x is zero and the namespace_or_type_name appears within a generic method declaration (§15.6) but outside the attributes of its method-header, and if that declaration includes a type
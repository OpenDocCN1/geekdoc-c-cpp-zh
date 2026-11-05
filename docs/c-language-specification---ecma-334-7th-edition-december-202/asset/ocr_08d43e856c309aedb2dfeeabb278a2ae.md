```
Y::N::B b2;
Y::N::C c;
}
```

The program declares the existence of the extern aliases X and Y, but the actual definitions of the aliases are external to the program. The identically named N::B classes can now be referenced as X::N::B and Y::N::B, or, using the namespace alias qualifier, X::N::B and Y::N::B. end example

# 14.5 Using directives

# 14.5.1 General

Using directives facilitate the use of namespaces and types defined in other namespaces. Using directives impact the name resolution process of namespace_or_type_names (§7.8) and simple_names (§12.8.4), but unlike declarations, using_directives do not contribute new members to the underlying declaration spaces of the compilation units or namespaces within which they are used.

```
using_directive
  : using_alias_directive
  | using_namespace_directive
  | using_static_directive
  ;
```

A using_alias_directive (§14.5.2) introduces an alias for a namespace or type.

A using_namespace_directive (§14.5.3) imports the type members of a namespace.

A using_static_directive (§14.5.4) imports the nested types and static members of a type.

The scope of a using_directive extends over the namespace_member_declarations of its immediately containing compilation unit or namespace body. The scope of a using_directive specifically does not include its peer using_directives. Thus, peer using_directives do not affect each other, and the order in which they are written is insignificant. In contrast, the scope of an extern_alias_directive includes the using_directives defined in the same compilation unit or namespace body.

# 14.5.2 Using alias directives

A using_alias_directive introduces an identifier that serves as an alias for a namespace or type within the immediately enclosing compilation unit or namespace body.

```
using_alias_directive
  : 'using' identifier '=' namespace_or_type_name ';'
  ;
```

Within global attributes and member declarations in a compilation unit or namespace body that contains a using_alias_directive, the identifier introduced by the using_alias_directive can be used to reference the given namespace or type.

Example:

```
namespace N1.N2
{
  class A {}
}
namespace N3
{
  using A = N1.N2.A;
```
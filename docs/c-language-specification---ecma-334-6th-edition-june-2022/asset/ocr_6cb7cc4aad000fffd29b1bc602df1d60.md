*unsafe_modifier* (§22.2) is only available in unsafe code (§22).

It is a compile-time error for the same modifier to appear multiple times in an interface declaration.

The *new* modifier is only permitted on interfaces defined within a class. It specifies that the interface hides an inherited member by the same name, as described in §14.4.3.5.

The *public*, *protected*, *internal*, and *private* modifiers control the accessibility of the interface. Depending on the context in which the interface declaration occurs, only some of these modifiers might be permitted (§7.5.2). When a partial type declaration (§14.2.7) includes an accessibility specification (via the *public*, *protected*, *internal*, and *private* modifiers), the rules in §14.2.2 apply.

# 17.2.3 Variant type parameter lists

# 17.2.3.1 General

Variant type parameter lists can only occur on interface and delegate types. The difference from ordinary *type_parameter_lists* is the optional *variance_annotation* on each type parameter.

```
variant_type_parameter_list
  : '<' variant_type_parameters '>'
  ;

variant_type_parameters
  : attributes? variance_annotation? type_parameter
  | variant_type_parameters ',' attributes? variance_annotation? type_parameter
  ;

variance_annotation
  : 'in'
  | 'out'
  ;
```

If the variance annotation is *out*, the type parameter is said to be *covariant*. If the variance annotation is *in*, the type parameter is said to be *contravariant*. If there is no variance annotation, the type parameter is said to be *invariant*.

*Example:* In the following:

```
interface C<out X, in Y, Z>
{
    X M(Y y);
    Z P { get; set; }
}
```

X is covariant, Y is contravariant and Z is invariant.

*end example*

If a generic interface is declared in multiple parts (§14.2.3), each partial declaration shall specify the same variance for each type parameter.

# 17.2.3.2 Variance safety

The occurrence of variance annotations in the type parameter list of a type restricts the places where types can occur within the type declaration.

A type T is *output-unsafe* if one of the following holds:

+   - T is a *contravariant* type parameter
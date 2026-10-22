Click here to view code image

```
template<typename T> void maybeDependent(T const& x)
{
sizeof(sizeof(x));
}
```

Here, the inner sizeof expression is value-dependent, as noted above. However, the outer sizeof expression always computes the size of a std::size_t, so both its type and constant value are consistent across all instantiations of the template, despite the innermost expression (x) being type-dependent. Any expression that involves a template parameter is an instantiation-dependent expression,¹³ even if both its type and constant value are invariant across valid instantiations. However, an instantiation-dependent expression may turn out to be invalid when instantiated. For example, instantiating maybeDependent() with an incomplete class type will trigger an error, because sizeof cannot be applied to such types.

Type-, value-, and instantiation-dependence can be thought of as a series of increasingly more inclusive classifications of expressions. Any type-dependent expression is also considered to be value-dependent, because an expression whose type that varies from one instantiation to the next will naturally have its constant value vary from one instantiation to the next. Similarly, an expression whose type or value varies from one instantiation to the next depends on a template parameter in some way, so both type-dependent expressions and value-dependent expressions are instantiation-dependent. This containment relationship is illustrated by Figure 13.1.

Click here to view code image

Figure 13.1. Containment relationship among type-, value-, and instantiation-dependent expressions

As one proceeds from the innermost context (type-dependent expressions) to the outermost context, more of the behavior of the template is determined when the template is parsed and therefore cannot vary from one instantiation to the next. For example, consider the call f(x): If x is type-dependent, then f is a dependent name that is subject to two-phase lookup (Section 14.3.1 on page 249), whereas if x is value-dependent but not type-dependent, f is a nondependent name for which name lookup can be completely determined at the time that the template is parsed.
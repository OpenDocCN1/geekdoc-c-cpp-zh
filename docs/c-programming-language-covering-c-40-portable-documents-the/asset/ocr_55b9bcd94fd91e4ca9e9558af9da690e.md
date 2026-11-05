# ### 13.1.3 Variant Type Parameter Lists

Variant type parameter lists can occur only on interface and delegate types. The difference from ordinary *type-parameter-lists* is the optional *variance-annotation* on each type parameter.

```
```
variant-type-parameter-list:
    < variance-type-parameters >

variance-type-parameters:
    attributes_opt variance-annotation_opt type-parameter
    variance-type-parameters , attributes_opt variance-annotation_opt type-parameter

variance-annotation:
    in
    out
```
```

If the variance annotation is out, the type parameter is said to be *covariant*. If the variance annotation is in, the type parameter is said to be *contravariant*. If there is no variance annotation, the type parameter is said to be *invariant*.

> > **ERIC LIPPERT** Covariance is the property that a mapping from a type argument to a generic type preserves assignment compatibility. For example, a string may be assigned to a variable of type object. A mapping from T to IEnumerable<T> preserves the assignment compatibility; an IEnumerable<string> can be assigned to a variable of IEnumerable<object>. Thus the nomenclature that "the type parameter is covariant" is a shorthand; the thing that is actually covariant is the relationship between the type argument and the constructed type. Properly we ought to say, "The mapping from—any reference type T to IEnumerable<T> is covariant in T" but that is rather a mouthful compared to simply saying, "T is covariant," and understanding that the longer statement is what is meant by it.

In the example

```
```csharp
interface C<out X, in Y, Z>
{
    X M(Y y);

    Z P { get; set; }
}
```
```

X is covariant, Y is contravariant, and Z is invariant.
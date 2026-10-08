This is ad hoc, but better than trying to correctly and consistently call free(p) on all exits from
t function.

The finally() function is trivial:

Click here to view code image

```
template <class F>
[[nodiscard]] auto finally(F f)
{
    return Final_action(f);
}
```

I used the [[nodiscard]] to ensure that users do not forget to copy a generated Final_Action
t the scope for its action is intended.
The class Final_action that supplies the necessary destructor can look like this:

Click here to view code image

```
template <class F>
struct Final_action {
    explicit Final_action(F f) : Final_action(f) {}
    ~Final_action() {};
};
```

There is a finally() in the Core Guidelines Support Library (the GSL) and a proposal for a more
elaborate scope_exit mechanism for the standard library.

# 7.4 Template Mechanisms

To define good templates, we need some supporting language facilities:

+   * Values depend on a type: variable templates (§7.4.1)
* Aliases for types and templates: aliases templates (§7.4.2)
* A compile-time selection mechanism: if constexpr (§7.4.3)
* A compile-time mechanism to inquire about properties of types and expressions: requires-expressions (§8.2.3).

In addition, constexpr functions (§1.6) and static_asserts (§4.5.2) often take part in template
design and use.
These basic mechanisms are primarily tools for building general, foundational abstractions.

# 7.4.1 Variable Templates

When we use a type, we often want constants and values of type. This is of course also the
case we use a class template: when we define a C<T>, we often want constants and
variables of type C<T> and other types depending on T. Here is an example from a fluid dynamic
sim [Garcia,2015]:

Click here to view code image
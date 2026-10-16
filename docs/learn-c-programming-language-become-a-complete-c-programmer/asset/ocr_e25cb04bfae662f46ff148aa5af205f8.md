The process of finding the declaration for each name explicitly or implicitly used in a template is called *name binding*. The general problem with template name binding is that three contexts are involved in a template instantiation and they cannot be cleanly separated:

+   [1] The context of the template definition
+   [2] The context of the argument type declaration
+   [3] The context of the use of the template

When defining a function template, we want to assure that enough context is available for the template definition to make sense in terms of its actual arguments without picking up “accidental stuff” from the environment of a point of use. To help with this, the language separates names used in a template definition into two categories:

+   [1] *Dependent names*: names that depend on a template parameter. Such names are bound at a point of instantiation (§26.3.3). In the **sum()** example, the definition of + can be found in the instantiation context because it takes operands of the template argument type.
+   
+   [2] *Nondependent names*: names that don’t depend on a template parameter. Such names are bound at the point of definition of the template (§26.3.2). In the **sum()** example, the template **vector** is defined in the standard header `<vector>`, and the Boolean **tracing** is in scope when the definition of **sum()** is encountered by the compiler.

To be considered, both dependent and independent names must either be in scope at their point of use or be found by argument-dependent lookup (ADL; §14.2.4).

The following subsections go into considerable technical detail about how dependent and nondependent names in a template definition are bound for a specialization. For complete details, see §iso.14.6.

# 26.3.1 Dependent Names

The simplest definition of “**N** depends on a template parameter **T**” would be “**N** is a member of **T**.” Unfortunately, this doesn’t quite suffice; addition of **QuadS** (§26.3) is a counter-example.

Consequently, a function call is said to *depend on* a template argument if and only if one of these conditions holds:

+   [1] The type of the actual argument depends on a template parameter **T** according to the type deduction rules (§23.5.2), for example, **f(T(1))**, **f(t)**, **f(g(t))**, and **f(&t)**, assuming that **t** is a **T**.
+   
+   [2] The function called has a parameter that depends on **T** according to the type deduction rules (§23.5.2), for example, **f(T)**, **f(list<T>&)**, and **f(const T\*)**.

Basically, the name of a called function is dependent if it is obviously dependent by looking at its arguments or at its formal parameters. For example:

```
template<typename T>
T f(T a)
{
```
3 A given type P can be composed from a number of other types, templates, and non-type values:

+   — A function type includes the types of each of the function parameters and the return type.

+   — A pointer-to-member type includes the type of the class object pointed to and the type of the member pointed to.

+   — A type that is a specialization of a class template (e.g., A<int>) includes the types, templates, and non-type values referenced by the template argument list of the specialization.

+   — An array type includes the array element type and the value of the array bound.

4 In most cases, the types, templates, and non-type values that are used to compose P participate in template argument deduction. That is, they may be used to determine the value of a template argument, and template argument deduction fails if the value so determined is not consistent with the values determined elsewhere. In certain contexts, however, the value does not participate in type deduction, but instead uses the values of template arguments that were either deduced elsewhere or explicitly specified. If a template parameter is used only in non-deduced contexts and is not explicitly specified, template argument deduction fails.

> [Note 1: Under 13.10.3.2, if P contains no template-parameters that appear in deduced contexts, no deduction is done, so P and A need not have the same form. — end note]

5 The non-deduced contexts are:

+   — The nested-name-specifier of a type that was specified using a qualified-id.

+   — The expression of a decltype-specifier.

+   — A non-type template argument or an array bound in which a subexpression references a template parameter.

+   — A template parameter used in the parameter type of a function parameter that has a default argument that is being used in the call for which argument deduction is being done.

+   — A function parameter for which the associated argument is an overload set (12.5), and one or more of the following apply:

+   — more than one function matches the function parameter type (resulting in an ambiguous deduction), or

+   — no function matches the function parameter type, or

+   — the overload set supplied as an argument contains one or more function templates.

+   — A function parameter for which the associated argument is an initializer list (9.4.5) but the parameter does not have a type for which deduction from an initializer list is specified (13.10.3.2).

> [Example 1:
> template<class T> void g(T);
> g({1,2,3}); // error: no argument deduced for T
> — end example]

+   — A function parameter pack that does not occur at the end of the parameter-declaration-list.

6 When a type name is specified in a way that includes a non-deduced context, all of the types that comprise that type name are also non-deduced. However, a compound type can include both deduced and non-deduced types.

> [Example 2: If a type is specified as A<T>::B<T2>, both T and T2 are non-deduced. Likewise, if a type is specified as A<I+J>::X<T>, I, J, and T are non-deduced. If a type is specified as void f(typename A<T>::B, A<T>), the T in A<T>::B is non-deduced but the T in A<T> is deduced. — end example]

7 [Example 3: Here is an example in which different parameter/argument pairs produce inconsistent template argument deductions:

```
template<class T> void f(T x, T y) { /* ... */ }
struct A { /* ... */ };
struct B : A { /* ... */ };
void g(A a, B b) {
    f(a,b); // error: T deduced as both A and B
    f(b,a); // error: T deduced as both A and B
    f(a,a); // OK: T is A
    f(b,b); // OK: T is B
}
```
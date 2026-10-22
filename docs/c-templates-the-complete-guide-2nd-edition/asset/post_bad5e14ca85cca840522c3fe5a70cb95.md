
## 12.2.5 Default Template Arguments

Any kind of template parameter that is not a template parameter pack can be equipped with a default argument, although it must match the corresponding parameter in kind (e.g., a type parameter cannot have a nontype default argument). A default argument cannot depend on its own parameter, because the name of the parameter is not in scope until after the default argument. However, it may depend on previous parameters:

```
template<typename T, typename Allocator = allocator<T>>
class List;
```

A template parameter for a class template, variable template, or alias template can have a default template argument only if default arguments were also supplied for the subsequent parameters. (A similar constraint exists for default function call arguments.) The subsequent default values are usually provided in the same template declaration, but they could also have been declared in a previous declaration of that template. The following example makes this clear:

```
template<typename T1, typename T2, typename T3,
typename T4 = char, typename T5 = char>
class Quintuple; // OK
```

```
template<typename T1, typename T2, typename T3 = char,
typename T4, typename T5>
class Quintuple; // OK: T4 and T5 already have defaults
```

```
template<typename T1 = char, typename T2, typename T3,
typename T4, typename T5>
class Quintuple; // ERROR: T1 cannot have a default argument
// because T2 doesn’t have a default
```

Default template arguments for template parameters of function templates do not require subsequent template parameters to have a default template argument:

```
template<typename R = void, typename T>
R* addressof(T& value); // OK: if not explicitly specified, R will be void
```

Default template arguments cannot be repeated:

```
template<typename T = void>
class Value;
```

```
template<typename T = void>
class Value; // ERROR: repeated default argument
```

A number of contexts do not permit default template arguments:
- Partial specializations:

```
template<typename T>
class C;
...
template<typename T = int>
class C<T*>; // ERROR
```
- Parameter packs:

```
template<typename... Ts = int> struct X; // ERROR
```
- The out-of-class definition of a member of a class template:

```
template<typename T> struct X
{
T f();
};

template<typename T = int> T X<T>::f() { // ERROR
...
}
```
- A friend class template declaration:

```
struct S {
template<typename = void> friend struct F;
};
```
- A friend function template declaration unless it is a definition and no declaration of it appears anywhere else in the translation unit:

```
struct S {
template<typename = void> friend void f(); // ERROR: not a definition
template<typename = void> friend void g() { //OK so far
}
};
template<typename> void g(); // ERROR: g() was given a default template argument
// when defined; no other declaration may exist here
```

## 12.3 Template Arguments

When instantiating a template, template parameters are substituted by template arguments. The arguments can be determined using several different mechanisms:
- Explicit template arguments: A template name can be followed by explicit template arguments enclosed in angle brackets. The resulting name is called a *template-id*.
- Injected class name: Within the scope of a class template X with template parameters P1, P2, ..., the name of that template (X) can be equivalent to the template-id X<P1, P2, ...>. See Section 13.2.3 on page 221 for details.
- Default template arguments: Explicit template arguments can be omitted from template instances if default template arguments are available. However, for a class or alias template, even if all template parameters have a default value, the (possibly empty) angle brackets must be provided.
- Argument deduction: Function template arguments that are not explicitly specified may be deduced from the types of the function call arguments in a call. This is described in detail in Chapter 15. Deduction is also done in a few other situations. If all the template arguments can be deduced, no angle brackets need to be specified after the name of the function template. C++17 also introduces the ability to deduce class template arguments from the initializer of a variable declaration or functional-notation type conversion; see Section 15.12 on page 313 for a discussion.

### 12.3.1 Function Template Arguments

Template arguments for a function template can be specified explicitly, deduced from the way the template is used, or provided as a default template argument.
For example:

*details/max.cpp*

```
template<typename T>
T max (T a, T b)
{
return b < a ? a : b;
}

int main()
{
::max<double>(1.0, -3.0); // explicitly specify template argument
::max(1.0, -3.0); // template argument is implicitly deduced to be
double
::max<int>(1.0, 3.0); // the explicit <int> inhibits the deduction;
// hence the result has type int
```

Some template arguments can never be deduced because their corresponding template parameter does not appear in a function parameter type or for some other reason (see Section 15.2 on page 271). The corresponding parameters are typically placed at the beginning of the list of template parameters so they can be specified explicitly while allowing the other arguments to be deduced. For example:

```
details/implicit.cpp

template<typename DstT, typename SrcT>
DstT implicit_cast (SrcT const& x) // SrcT can be deduced, but DstT cannot
{
    return x;
}

int main()
{
    double value = implicit_cast<double>(-1);
}
```

If we had reversed the order of the template parameters in this example (in other words, if we had written `template<typename SrcT, typename DstT>`), a call of `implicit_cast` would have to specify both template arguments explicitly.

Moreover, such parameters can’t usefully be placed after a template parameter pack or appear in a partial specialization, because there would be no way to explicitly specify or deduce them.

```
template<typename ... Ts, int N>
void f(double (&)[N+1], Ts ... ps); // useless declaration because N
                                     // cannot be specified or deduced
```

Because function templates can be overloaded, explicitly providing all the arguments for a function template may not be sufficient to identify a single function: In some cases, it identifies a set of functions. The following example illustrates a consequence of this observation:

```
template<typename Func, typename T>
void apply (Func funcPtr, T x)
{
    funcPtr(x);
}
```

```
template<typename T> void single(T);

template<typename T> void multi(T);
template<typename T> void multi(T*);

int main()
{
apply(&single<int>, 3); // OK
apply(&multi<int>, 7); // ERROR: no single multi<int>
}
```

In this example, the first call to `apply()` works because the type of the expression `&single<int>` is unambiguous. As a result, the template argument value for the `Func` parameter is easily deduced. In the second call, however, `&multi<int>` could be one of two different types and therefore `Func` cannot be deduced in this case.

Furthermore, it is possible that substituting template arguments in a function template results in an attempt to construct an invalid C++ type or expression. Consider the following overloaded function template (RT1 and RT2 are unspecified types):

```
template<typename T> RT1 test(typename T::X const*);
template<typename T> RT2 test(...);
```

The expression `test<int>` makes no sense for the first of the two function templates because type `int` has no member type `X`. However, the second template has no such problem. Therefore, the expression `&test<int>` identifies the address of a single function. The fact that the substitution of `int` into the first template fails does not make the expression invalid. This SFINAE (substitution failure is not an error) principle is an important ingredient to make the overloading of function templates practical and is discussed in Section 8.4 on page 129 and Section 15.7 on page 284.

### 12.3.2 Type Arguments

Template type arguments are the “values” specified for template type parameters. Any type (including `void`, function types, reference types, etc.) can, in general, be used as a template argument, but their substitution for the template parameters must lead to valid constructs:

```
template<typename T>
void clear (T p)
{
*p = 0; // requires that the unary * be applicable to T
}
```

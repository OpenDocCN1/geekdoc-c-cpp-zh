name, we don't know whether it's the name of a type, a template, or something else.

[Click here to view code image](#)

```
```cpp
template<typename T>
class X {
 public:
   using MyType = T;
   template<typename U>
   struct Magic;
};
```
```

Again, if we want a dependent name to be brought in by a using declaration to denote a type, we must explicitly say so by inserting the keyword `typename`. Strangely, the C++ standard does not provide for a similar mechanism to mark such dependent names as templates. The following snippet illustrates the problem:

[Click here to view code image](#)

```
```cpp
template<typename T>
class X {
 public:
   using B = X<T>::template Magic; // error: not a standard
};
```
```

The standardization committee has not been inclined to address this issue. However, C++11 alias templates do provide a partial workaround:

[Click here to view code image](#)

```
```cpp
template<typename T>
class X {
 public:
   template<typename U>
   using Magic = X<T>::template Magic<U>;
};
```
```

This is a little unwieldy, but it achieves the desired effect for the case of class templates. The case of function templates (arguably less common) remains unaddressed, unfortunately.

# 13.3.5 ADL and Explicit Template Arguments

Consider the following example:

[Click here to view code image](#)

```
```cpp
namespace X {
  class X {
  };
  template<int I> void select(X*);
}

void g (X::X* xp) {
  select<3>(xp);  // ERROR: no ADL!
}
```
```

In this example, we may expect that the template `select<>` is found through ADL in the call `select<3>(xp)`. However, this is not the case because a certain amount of code that is a function call argument will not be parsed until it has decided that `<3>` is a template argument list. Furthermore, a compiler cannot decide that `<3>` is a template argument list until it has found `select` (to be a template). Because this chicken-and-egg problem cannot be resolved, the expression is parsed as `select < 3 > (xp)`, which makes no sense.

This example may give the impression that ADL is disabled for template-ids, but it is not. The code can be fixed by introducing a function template that is named `select` within the call:

[Click here to view code image](#)

```
```cpp
template<typename T>
void select(T);

void g (X::X* xp) {
  select<>(xp);
}
```
```

Even though it doesn't make any sense for the call `select<>(xp)`, the presence of this function template ensures that `select<>` will be parsed as a template-id. ADL will then find the function template `X::select`, and the call will succeed.

# 13.3.6 Dependent Expressions

Like names, expressions themselves can be dependent on template parameters. An expression that depends on a template parameter can behave differently from one instantiation to the next—for example, selecting a different overloaded function or producing a different type or constant value. Expressions that do not depend on a template parameter, in contrast, are constant, and provide the same behavior in all instantiations.

An expression can be dependent on a template parameter in several dif-
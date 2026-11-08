class template because the size of `C<void>` is needed.

`C<void*> p = new C<void*>;`

In this case, instantiation is needed so that the compiler can determine the size of `C<void>`, which the next expression needs to determine how much storage to allocate. You might observe that for this particular template, the type of the argument `X` associated for `T` is not influence the size of the template because any non-zero `void*` argument is always nonzero. However, a compiler is not required to avoid instantiation by analyzing the template definition (and all compilers do perform the instantiation in practice). Furthermore, instantiation is also needed in this example to determine whether `C<void>` has an accessible default constructor and to ensure `C<void>` does not declare member operator `new` or `delete`.

The need to access a member of a class template is not always very explicitly visible in the source code. For example, C++ overload resolution requires visibility into class types for parameters of candidate functions:

Click here to view code image

```
template<typename T>
class C {
 public:
  C();              // a constructor that can be called
                     // with a single parameter
  T x;              // may be used for implicit conver-
                     // sions

  void candidate(C<double>);  // #1
  void candidate(C<int>);     // #2
};

int main()
{
  candidate(42);     // both previous function declara-
                     // tions can be called
}
```

The call `candidate(42)` will resolve to the overloaded declaration at point #2. However, the declaration at point #1 could also be instantiated to check whether it is a viable candidate for the call (it is in this case because the class-template constructor can implicitly convert `int` to a value of type `C<double>`). Note that the compiler is allowed (but not required) to perform this instantiation if it can resolve the call without it (as could be the case in this example because an implicit conversion would not be needed over an exact match). Note also that the instantiation of `C<double>` would trigger an error, which may be surprising.

# 14.2 LAZY INSTANTIATION

The examples so far illustrate requirements that are not fundamentally different from the requirements when using non-simple classes. Many users require a class type to be complete (see Section 3.0.1 on page 154). For the template case, the compiler will generate that complete definition from that class template definition.

A pertinent question now arises: How much of the template is instantiated? A proper answer is the following: Only as much as is really needed. In other words, a compiler should be “lazy” when instantiating templates. Let’s look at exactly what this laziness entails.

# 14.2.1 Partial and Full Instantiation

As we have seen, the compiler sometimes doesn’t need to substitute the complete definition of a class or function template. For example:

Click here to view code image

```
template<typename T>
decltype(T{2} ? T{1} : T{0}) f();
```

In this example, the type indicated by `decltype(f(2))` does not require the complete instantiation of the function template `f()`. A compiler is therefore only permitted to substitute the declaration of `f()`, but not its body. This is sometimes called partial instantiation.

Similarly, if an instance of a class template is referred to without the need for that instance to be a complete type, the compiler should not perform a complete instantiation of that class template instance. Consider the following example:

Click here to view code image

```
template<typename T> class Q {
  using Type = typename T::Type;
};

Q<int>* p = 0;     // Ok: the body of Q<int> is not sub-
                   // stituted
```

Here, the full instantiation of `Q<int>` would trigger an error, because `T::Type` doesn’t make sense when `T` is `int`. But because `Q<int>` does not need to be complete in this example, no full instantiation is performed and the code is okay (albeit suspicious).

Variable templates also have a “full” instantiation distinction. The following example illustrates it:

Click here to view code image

template<typename T> T v = T::default_value();

A full instantiation of `v<T>` would elicit an error, but that is not needed if we only read the type of the variable template instance.

Interestingly, alias templates do not have this distinction: There are no
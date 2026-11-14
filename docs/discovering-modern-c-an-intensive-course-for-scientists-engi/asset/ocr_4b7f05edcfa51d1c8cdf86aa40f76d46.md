However, most errors we encounter depend on the substituted types. For instance, the following implementation would compile:

```
template <typename T>
inline T max(T x, T y)
{
    return x < y ? y.value : x.value;
}
```

We could not call it with any intrinsic type like int or double, but the function template might not be intended for intrinsic types and may work with the actual argument types.

The compilation of the function template itself does not generate any code in the binary. This only happens when we call it. In this case, we instantiate this function template. Only then the compiler performs a complete check of whether the generic function is correct for the given argument type(s). In our previous examples, we saw that max can be instantiated with int and double.

So far, we have seen the most implicit form: the template is instantiated when a call exists and the type parameter is deduced from the arguments. To be more explicit, we can declare the type that substitutes the template parameter, e.g.:

```
std::cout << max<float>(8.1, 9.3) << '\n';
```

Here, the template is explicitly instantiated with a given type. In the most explicit form, we force an instantiation without a function call:

```
template short max<short>(short, short);
```

This can be useful when we generate object files (§7.2.1.3) and must guarantee that certain instances are present, regardless of the function calls in the compile unit.

> Definition 3-1. For conciseness, we call an instantiation with type deduction Implicit Instantiation and an instantiation with an explicit type declaration Explicit Instantiation.

In our experience, implicit instantiation works in most cases as expected. The explicit nomination of the instantiation type is mostly needed for disambiguation and special usages like std::forward (§3.1.2.4). For a deeper understanding of templates, it is very helpful to know how the compiler substitutes the types.

# 3.1.2 Parameter Type Deduction

```
=> c++11/template_type_deduction.cpp
```

In this section, we will have a closer look at how template parameters are substituted depending on whether the arguments are passed by value, value, or rvalue reference. This knowledge is even more important when variables are declared with an automatic type via auto as shown in Section 3.4.1. However, the substitution rules are more intuitive with function parameters than with auto variables and we therefore discuss them here.
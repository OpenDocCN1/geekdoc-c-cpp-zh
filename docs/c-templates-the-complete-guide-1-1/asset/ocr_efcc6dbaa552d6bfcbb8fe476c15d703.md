# Chapter 15

# Template Argument Deduction

Explicitly specifying template arguments on every call to a function template (e.g., `concat<int, string, int>(...)`) can quickly lead to unwieldy code. Fortunately, a C++ compiler often can automatically determine the intended template arguments using a powerful process called template argument deduction.

In this chapter we explain the details of this template argument deduction process. As is often the case in C++, there are many rules that usually provide an intuitive result. A solid understanding of this chapter allows us to avoid the more surprising situations.

Although template argument deduction was first developed to ease the invocation of function templates, it has since been broadened to apply to several other uses, including determining the types of variables from their initializers.

# 15.1 THE DEDUCTION PROCESS

The basic deduction process compares the types of an argument of a function call with the corresponding parameterized type of a function template and attempts to conclude the correct substitution for one or more of the deduced parameters. Each argument-parameter pair is analyzed independently, and if the conclusion differs in the end, the deduction process fails. Consider the following example:

Click here to view code image

```
template<typename T>
T max (T a, T b)
{
    return b < a ? a : b;
}

auto x = max(1, 1.0);
```

Here the first call argument of type `int` causes the parameter `T` of our original `max()` template to be automatically deduced to be `int`. The second call argument is a `double`, however, and so `T` should be `double` for this argument. This conflicts with the previous conclusion. Note that we say that “the deduction process fails,” not that “the program is invalid.” After all, it is possible that the deduction process would succeed for another template overload (maximum function template can be overloaded much like ordinary functions; see Section 5.2.9 and Chapter 16).

If all the deduced template parameters are consistently determined, the deduction process can still fail if substituting the arguments in the rest of the function declaration results in an invalid construct. For example:

Click here to view code image

```
template<typename T>
typename T::ElementT max (T a, int)
{
    return a[1];
}

void f(int* p)
{
    int x = f(p);
}
```

Here `T` is concluded to be `int*` (there is only one parameter type where `T` appears, so there are obviously no analysis conflicts). However, substituting `int*` for `T` in the return type `T::ElementT` is clearly invalid C++, and deduction process fails.

We still need to explore how argument-parameter matching proceeds. We describe it in terms of matching a type A (derived from the call argument) to a parameterized type P (derived from the call parameter declaration). If the call parameter is declared with a reference or pointer, P is taken to be the type referred, and A is the type of the argument. Otherwise, however, P is the declared parameter type, and A is obtained from the type of the argument by decaying array and function types to pointer types, ignoring top-level const and volatile qualifiers. For example:

Click here to view code image
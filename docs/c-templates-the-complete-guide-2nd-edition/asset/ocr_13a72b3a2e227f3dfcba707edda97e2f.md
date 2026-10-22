Note also that the same rules apply to variadic function template parameters as for ordinary parameters. For example, if passed by value, arguments are copied and decay (e.g., arrays become pointers), while if passed by reference, parameters refer to the original parameter and don’t decay: Click here to view code image

```
// args are copies with decayed types:
template<typename... Args> void foo (Args... args);
// args are nondecayed references to passed objects:
template<typename... Args> void bar (Args const&... args);
```

# 4.4 Variadic Class Templates and Variadic Expressions

Besides the examples above, parameter packs can appear in additional places, including, for example, expressions, class templates, using declarations, and even deduction guides. Section 12.4.2 on page 202 has a complete list.

# 4.4.1 Variadic Expressions

You can do more than just forward all the parameters. You can compute with them, which means to compute with all the parameters in a parameter pack.
For example, the following function doubles each parameter of the parameter pack args and passes each doubled argument to print(): Click here to view code image

```
template<typename... T>
void printDoubled (T const&... args)
{
print (args + args...);
}
```

If, for example, you call Click here to view code image

```
printDoubled(7.5, std::string("hello"), std::complex<float>(4,2));
```

the function has the following effect (except for any constructor side effects):
Click here to view code image

```
print(7.5 + 7.5,
std::string("hello") + std::string("hello"),
std::complex<float>(4,2) + std::complex<float>(4,2); If you just want
```
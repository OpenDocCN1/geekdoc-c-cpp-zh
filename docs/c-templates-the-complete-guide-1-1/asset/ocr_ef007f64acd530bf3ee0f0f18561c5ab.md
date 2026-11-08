For all these reasons, the best and easiest solution is to let the compiler deduce the return types as proposed in Section 1.3.2 on page 11.

# 1.5 OVERLOADING FUNCTION TEMPLATES

Like ordinary functions, function templates can be overloaded. That is, you can have different function definitions with the same function name so that when that name is used in a function call, a C++ compiler must decide which one of the various candidates to call. The rules for this decision may become rather complicated, even without templates. In this section we discuss overloading when templates are involved. If you are not familiar with the rules of function overloading without templates, please look at Appendix C, where we provide a reasonably detailed survey of the overloaded resolution rules.

The following short program illustrates overloading a function template:

Click here to view code image

```
```cpp
// maximum of two int values:

int max (int a,
         int b)
{
    return b < a ? a : b;
}

// maximum of two values of any type:

template<typename T>
T max (T a, T b)
{
    return b < a ? a : b;
}

int main()
{
    ::max(7, 42);          // calls the nontemplate
    ::max(7, 42.0);        // calls max<double>
    ::max('a', 'b');       // calls max<char>
    ::max(7.0, 42);        // calls max<double>
    ::max<double>(7, 42);  // calls the nontemplate
}
```
```

As this example shows, a non-template function can coexist with a function template that has the same name and can be instantiated with the same type. All other factors being equal, the overload resolution process prefers the non-template over one generated from the template. The first call falls under this rule:

Click here to view code image

```
```cpp
::max(7, 42);    // both int values match the nontemplate function perfectly
```
```

If the template can generate a function with a better match, however, then the template is selected. This is demonstrated by the second and third calls of max():

Click here to view code image

```
```cpp
::max(7, 42.0);    // calls the max<double> by argument deduction
::max('a', 'b');    // calls the max<char> by argument deduction
```
```

Here, the template is a better match because no conversion from double or char to int is required (see Section C.2 on page 682 for the rules of overload resolution).
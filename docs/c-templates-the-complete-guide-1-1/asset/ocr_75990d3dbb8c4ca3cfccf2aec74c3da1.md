However, in this sort of case, an additional overload resolution criterion comes into play: The function generated from the more specialized template is selected. Here (as we see shortly), the second template is considered more specialized and thus the output of our example is

# 16.2.3 Formal Ordering Rules

In our last example, it may seem very intuitive that the second template is more special than the first because the first can accommodate just about any argument type, whereas the second allows only pointer types. However, other examples are not necessarily as intuitive. In what follows, we describe the exact procedure to determine whether one function template is more participating in an overload set is more specialized than the other. Note that there are partial ordering rules: It is possible that given two templates, neither can be considered more specialized than the other. If a proposed resolution must select between two such templates, no decision can be made, and the program becomes ambiguous.

Let's assume we are comparing two identically named function templates that seem viable for a given function call. Overload resolution is divided as follows:

+   - Function call parameters that are covered by a default argument and all template parameters that are not used in a call are ignored in what follows.
+   - When synthesizing a function type for argument types (or conversion-function templates, a return type), every template parameter is substituted by an invented type.

+   1. Replace each template type parameter with a unique invented type.
+   2. Replace each template template parameter with a unique invented class template.
+   3. Replace each non-type template parameter with a unique invented value of the appropriate type. (Types, other types, templates, and values that are invented in this context are distinct from any other types, templates, or values that are defined in the programmer's source or synthesized in other contexts.)
+   
+   - If template argument deduction of the second template against the first instantiated function succeeds with one argument, but not vice versa, then the first template is more specialized than the second.

Let's consider a more concrete example illustrating multi-function parameters:

**Click here to view code image**

```
template<typename T>
void f(T, T* = nullptr, ...);

template<typename T>
void f(T const*, T* = nullptr);

void example(int* p)
{
    f(p, p);
}
```

First, because the actual call does not use the ellipsis parameter for the first template and the last parameter of the second template is covered by its default argument, these parameters are ignored in the partial ordering. Note that the default argument of the first template is not used; hence the corresponding parameter participates in the partial ordering.

The synthesized lists of argument types are (A1, A1 const*) and (A2 const*, A2). Template argument deduction of A1 against A2 const* versus the second template actually succeeds with the substitution of T with A1 const*, but the resulting match is not exact because a qualification adjustment is needed to call it const* (A1 const*, A1 const*) with arguments of type (A1*, A1 const*). Similarly, no exact match can be found by deducing template parameters for the first template from the argument type list (A2 const*, A2). Therefore, there is no ordering relationship between the two template parameters, and the call is ambiguous.

The formal ordering rules generally result in the intuitive selection of function templates. Once in a while, however, an example comes up for which the rules do not select a template choice. It is therefore possible that the rules will reject a template invocation that seems to have the future.

# 16.2.4 Templates and Nontemplates

Function templates can be overloaded with nontemplate functions. All being equal, the non-template function is preferred in selecting the actual function being called. The following example illustrates this:
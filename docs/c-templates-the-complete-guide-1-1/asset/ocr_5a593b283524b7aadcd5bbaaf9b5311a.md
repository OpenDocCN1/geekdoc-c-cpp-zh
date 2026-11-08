A template argument list would normally succeed by substituting A2 for T. In the other direction, deduction of this third template against the first's synthesized argument list succeeds by substituting the single-element sequence (A) for the parameter pack P. Partial ordering between the first and third templates would normally result in an ambiguity. However, a special rule prohibits an argument that originally came from a function parameter pack (e.g., the third template's parameter pack T...) from matching a parameter pack (e.g., the first template's parameter pack).

Hence, template deduction of the first template against the third's synthesized argument list fails, and the first template is considered more specialized than the third. This special rule effectively considers nonvariadic templates (those with a fixed number of parameters) to be more specialized than their variadic template counterparts.

The rules described above apply equally to pack expansions that occur in types in the function signature. For example, we can wrap the parameters as arguments of each of the function templates in our previous example into a variadic class template Tuple to arrive at a similar example not involving function parameter packs:

# Click here to view code image

details/tupleoverload.cpp

```
template <typename T>

template<typename... Ts> class Tuple
{

};

template<typename T>
int f(Tuple<T>)
{
    return 1;
}

template<typename... Ts>
int f(Tuple<Ts...>)
{
    return 2;
}

template<typename... Ts>
int f(Tuple<Ts...>)
{
    return 1;
}

int main()
{
    std::cout << f(Tuple<int, double>{});    // calls f
    std::cout << f(Tuple<int, double>{});    // calls f
    std::cout << f(Tuple<int>{});            // calls f
}
```

Function template ordering considers the pack expansions in the template arguments to Tuple analogously to the function parameter packs in our previous example, resulting in the same output:

# 16.3 EXPLICIT SPECIALIZATION

The ability to overload function templates, combined with the partial ordering rules to select the “best” matching function template, allows us to do some specialized templates to a generic implementation to use code appropriately for greater efficiency. However, class templates are variable templates cannot be overloaded; instead, partial specialization was chosen to enable transparent customization of class templates: explicit specialization of a class template is analogous to the function template specialization. For example, a programmer might want to provide a specialized template for a template with template parameters that are fully substituted. No template parameters remain. Class templates, function templates, and variable templates can be fully specialized.

So can members of class templates that may be defined outside the body of a class definition (i.e., member functions, nested data members, and member enumeration types).
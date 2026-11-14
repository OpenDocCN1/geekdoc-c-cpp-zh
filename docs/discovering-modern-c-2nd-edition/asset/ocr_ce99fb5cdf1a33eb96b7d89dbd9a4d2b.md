```
{
    using type= ThenType;
};

template <typename ThenType, typename ElseType>
struct conditional<false, ThenType, ElseType>
{
    using type= ElseType;
};
```

When this template is instantiated with a logical expression and two types, only the primary template (on top) matches when the first argument evaluates to true and ThenType is used in the type definition. If the first argument evaluates to false, then the specialization (below) is more specific so that ElseType is used. Like many ingenious inventions it is very simple once it is found. This meta-function is part of C++11 in the header <type_traits>.

5. With C++03, you can use boost::mpl::if_c from Boost's Meta-Programming Library (MPL). If you program with both the standard and Boost type traits, pay attention to the different naming conventions.

This meta-function allows us to define funny things like using double for temporaries when our maximal iteration number is larger than 100, otherwise float:

Click here to view code image

```
using tmp_type=
    typename conditional<(max_iter > 100), double,
    float>::type;
cout << "typeid = " << typeid(tmp_type).name() << '\n';
```

Needless to say, max_iter must be known at compile time. Admittedly, the example does not look extremely useful and the meta-if is not so important in small isolated code snippets. In contrast, for the development of large generic software packages, it becomes extremely important. Please note that the comparison is surrounded by parentheses; otherwise the greater-than symbol > would be interpreted as the end of the template arguments. Likewise, expressions containing right shift >> must be surrounded by parentheses in C++11 or higher for the same reason.
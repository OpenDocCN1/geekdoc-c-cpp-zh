# Template Aliases (C++11)

It can be convenient, especially in template design, to create aliases for types.You can use typedef to create aliases for template specializations:

```
// define typedef aliases
type std::array<double, 12> arrd
type std::array<int, 12> arri
type std::array<std::string, 12> arstr
arrd gallons // type std::array<double, 12
arri days // type std::array<int, 12
arrst months // type std::array<std::string, 12>
```

But if you find yourself writing code similar to the preceding typedefs, over and over, you might wonder if you've forgotten some language feature that simplifies the task or if the language has forgotten to supply such a feature. In this case, C++11 provides a feature previously missing—a way to use a template to provide a family of aliases. Here's what the approach looks like:

```
template<typename T>
using array = std::array<T,12>; // template create multiple aliases
```

This makes array a template alias that can be used as a type, as follows:

```
arrtype<double> gallons // type std::array<double, 12
arrtype<int> days // type std::array<int, 12>
arrtype<std::string> months // type std::array<std::string, 12
```

In short, array<T> makes type std::array<T,12>.
C++11 extends the using syntax to non-templates too. In that case, it becomes equivalent to an ordinary typedef:

```
typedef const char *; // typedef syntax
using po2 const char *; // using = syntax
def const int (*pa1)[10]; // typedef syntax
using pa2 const int (*)[10]; // using = syntax
```

As you used it, you may find the new form more readable because it separates the type name from information more clearly.
Another C++11 addition to templates is the variadic template, which allows you to define a template class or function that can take a variadic number of initializers. Chapter 18, "Visiting with the New C++ Standard," looks into this topic.

# Summary

C++ provides several means for reusing code. Public inheritance, described in Chapter 13,"Inheritance enables you to model is-a relationships, with derived classes able to reuse the code of base classes. Private and protected inheritance also lets you reuse base-class code, this type modeling has-a relationships. With private inheritance, public
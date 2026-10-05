# Allowed Non-generic Template Parameters

Non-generic parameters in templates are restricted to integers, pointers, or references. Other types, such as double and float, are not allowed. This restriction has been loosened in Modern C++.

# Using Default Arguments With Class Templates

A generic type in a class template can specify a default type. For example:

```
template <class Type=int>
Foo;
Foo<> foo; // the default type will be used
```

Default values are specified using the = syntax.

It is also permissible for non-generic arguments to have default values in a class declaration. The default value of the non-generic parameter will be used when an explicit value is not specified for the non-generic parameter when a particular template class is instantiated.

```
template <class tType=int, int size=10>
class Foo;
Foo<> foo;
```

Here, tType defaults to int, and size defaults to 10. Notice how the class Foo is declared with <>, means that Foo uses the default template parameters.

# Explicit Class Specializations

When a particular class object is instantiated from a class template (using specific type parameters and non-parameter values) we say that we have a specialization of the
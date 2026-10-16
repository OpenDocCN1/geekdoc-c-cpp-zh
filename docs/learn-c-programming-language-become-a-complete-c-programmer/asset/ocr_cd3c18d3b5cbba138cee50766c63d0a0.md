```
```cpp
vector<decltype (*beg)> v {beg,end}; // initialize a vector from [beg:end)
sort(v.begin(),v.end());
copy(v.begin(),v.end(),beg); // copy the elements back
}
```
```

The **decltype()** is a built-in type function that returns the declared type of its argument (§6.3.6.3). Thus, **v** is a **vector<X>** where X is the element type of the input sequence.

The real “type magic” is in the selection of helper functions:

```
```cpp
template<typename C>
void sort(C& c)
{
    using Iter = Iterator_type<C>;
    sort_helper(c.begin(),c.end(),Iterator_category<Iter>{});
}
```
```

Here, I use two type functions: **Iterator_type<C>** returns the iterator type of **C** (that is, **C::iterator**) and then **Iterator_category<Iter>{}** constructs a “tag” value indicating the kind of iterator provided:

+   - **std::random_access_iterator_tag** if C’s iterator supports random access.
+   - **std::forward_iterator_tag** if C’s iterator supports forward iteration.

Given that, we can select between the two sorting algorithms at compile time. This technique, called *tag dispatch* is one of several used in the standard library and elsewhere to improve flexibility and performance.

The standard-library support for techniques for using iterators, such as tag dispatch, comes in the form of a simple class template **iterator_traits** from **<iterator>** (§33.1.3). This allows simple definitions of the type functions used in **sort()**:

```
```cpp
template<typename C>
using Iterator_type = typename C::iterator; // C’s iterator type
template<typename Iter>
using Iterator_category = typename std::iterator_traits<Iter>::iterator_category; //
Iter’s category
```
```

If you don’t want to know what kind of “compile-time type magic” is used to provide the standard-library features, you are free to ignore facilities such as **iterator_traits**. But then you can’t use the techniques they support to improve your own code.

# 5.4.2.2 Type Predicates

A standard-library type predicate is a simple type function that answers a fundamental question about types. For example:

```
```cpp
bool b1 = Is_arithmetic<int>(); bool b2 = Is_arithmetic<string>();
// yes,int is an arithmetic type
// no,std::string is not an arithmetic type
```
```

These predicates are found in **<type_traits>** and described in §35.4.1. Other examples are **is_class**, **is_pod**, **is_literal_type**, **has_virtual_destructor**, and **is_base_of**. They are most useful when we write templates. For example:
# Chapter 5

# Tricky Basics

This chapter covers some further basic aspects of templates that are relevant to practical use of templates: an additional use of the `typename` keyword, defining member functions and nested classes as templates, template template parameters, zero initialization, and some details about using string literals as arguments for function templates. These aspects can be tricky at times, but every day-to-day programmer should have heard of them.

# 5.1 KEYWORD TYPENAME

The keyword `typename` was introduced during the standardization of C++ to clarify that an identifier inside a template is a type. Consider the following example:

Click here to view code image

```
```cpp
template<typename T>
class MyClass {
 public:
   ...
   void foo() {
     typename T::SubType* ptr;
     ...
   }
};
```
```

Here, the second `typename` is used to clarify that `SubType` is a type definition within class `T`. Thus, `ptr` is a pointer to the type `T::SubType`.

Without `typename`, `SubType` would be assumed to be a nontype member (e.g., a static data member or an enumerated constant). As a result, the expression

```
```cpp
T::SubType* ptr
```
```

would be a multiplication of the static `SubType` member of class `T` with `ptr`, which is not an error, because for some instantiations of `MyClass<T>` this could be valid code.

In general, `typename` has to be used whenever a name that depends on a template parameter is a type. This is discussed in detail in Section 13.3.2 on page 228.

One application of `typename` is the declaration to iterators of standard containers in generic code.

Click here to view code image

`basics/printcoll.cpp`

```
```cpp
#include <iostream>

// print elements of an STL container
template<typename T>
void printcoll (T const& coll)
{
    typename T::const_iterator pos;  // iterator to current element
    for (pos=coll.begin(); pos != coll.end(); ++pos) {
        std::cout << *pos << '\n';
    }
}
```
```

In this function template, the call parameter is a standard container of
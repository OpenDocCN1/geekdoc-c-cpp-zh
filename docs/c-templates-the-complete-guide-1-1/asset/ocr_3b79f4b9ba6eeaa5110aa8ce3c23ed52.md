# # Chapter 20

# ## Overloading on Type Properties

Function overloading allows the same function name to be used for multiple types, as long as those functions are distinguished by their parameter types. For example:

```
```cpp
void f (int);
void f (double);
void f (char const*);
```
```

With function templates, one can overload on type patterns such as pointer-to-T or T[]:

```
```cpp
template<typename T> void f (T*);
template<typename T> void f (T[]);
```
```

Given the prevalence of type traits (discussed in Chapter 19), it is natural to want to overload function templates based on the properties of the type template arguments. For example:

Click here to view code image

```
```cpp
template<typename T, typename... Ts>
void f (std::pair<T, Ts> const&); // only for pair
template<typename T, typename... Ts>
void f (std::vector<T, Ts> const&); // only for vectors
```
```

However, C++ does not currently provide any direct way to express overloads based on type properties. In fact, the two function templates immediately above are actually declarations of the same function template, rather than distinct overloads, because the names of template parameters are ignored when comparing two function templates.

Fortunately, there are a number of techniques that can be used to emulate overloading of function templates based on type properties. These techniques, as well as the common motivations for such overloading, are discussed in this chapter.

# ## 20.1 ALGORITHM SPECIALIZATION

One of the common motivations behind overloading of function templates is to provide more specialized versions of an algorithm based on knowledge of the types involved. Consider a simple swap() operation to exchange two values:

Click here to view code image

```
```cpp
template<typename T>
void swap (T& a, T& b)
{
  T tmp(a);
  a = b;
  b = tmp;
}
```
```

This implementation involves three operations for any type T; however, we can provide a more efficient swap() operation, such as for an Array<T> that stores its data as a pointer to the array contents and a length:

Click here to view code image

```
```cpp
template<typename T>
void swap (Array<T>& a, Array<T>& b)
{
  swap(a.ptr, b.ptr);
  swap(a.len, b.len);
}
```
```

Both implementations of swap() will correctly exchange the contents of two Array<T> objects. However, the latter implementation is more efficient, because it performs only two operations instead of three and all operations are pointer/length, and therefore, no additional operations for T are required. Note also that this is not available for an arbitrary type. The latter function template is therefore (conceptually) more specialized than the former, because it performs the same operation for a subset of the types accepted by the former function template. Finally, the second function template is also more specialized based on the particular rules for function template overloading (that is, partial ordering): It is a more specialized template (and, therefore, more efficient) function template when it is applicable.
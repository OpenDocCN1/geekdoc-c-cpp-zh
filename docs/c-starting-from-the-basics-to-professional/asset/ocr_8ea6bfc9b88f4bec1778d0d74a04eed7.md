```
```cpp
// A trailing return type constraining an abbreviated template’s parameter type
template <std::forward_iterator Iter>
Iter find_optimum(Iter begin, Iter end, auto compare)
    requires std::indirect_strict_weak_order<decltype(compare), Iter>;
```
```

# Constrained Class Templates

Constraining class templates is completely analogous to constraining function templates. And since most class templates, even the most basic ones, cannot be instantiated for just any type either, it is good practice to constrain most class template parameters as well.

In Chapter 17 we developed a simple Array<> template. You may recall that while doing so, we actually already mentioned most of the requirements for its type parameter. It’s now just a matter of translating these requirements into constraints, and preferably into concept expressions. Here is the outline of such a constrained Array<> template:

```
```cpp
template <typename T> requires std::default_initializable<T> && std::destructible<T>
class Array
{
public:
  explicit Array(size_t size);
  ~Array();
  // ...
};
```
```

To create a dynamic array of type T with operator new[], this type needs to be default-initializable. This rules out types without an accessible default constructor, as well as reference types and types such as void. To be able to later delete[] this array again, the type’s destructor must be public and non-deleted as well. (As mentioned before, std::destructible<> additionally requires this destructor to be noexcept, but that is something we are most definitely okay with.)

These are templates for members of Array<> that each rely on one of these constraints:

```
```cpp
template <typename T> requires std::default_initializable<T> && std::destructible<T>
Array<T>::Array(size_t size) : m_elements{new T[size]}, m_size {size}
{}
```
```

```
```cpp
template <typename T> requires std::default_initializable<T> && std::destructible<T>
Array<T>::~Array() { delete m_elements; }
```
```

The main thing to note here is that you have to repeat the requires clause of a constrained class template in the definitions of the templates for its members (even though at least one major compiler allows you to omit this, the C++ standard requires you to repeat the entire template head).
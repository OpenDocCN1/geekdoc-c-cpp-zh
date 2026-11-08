
```cpp
#include <iostream>
#include <array>

template<int N>
std::array<int, N> arr{};        // array with N elements, zero-initialized
template<int SD>
std::array<int, SD> value{};     // type of global variable depends on passed value

int main()
{
    std::cout << "The char" << '\n';       // it has value 0 for type char
    std::cout << arr[0] << '\n';
    // first element of global arr
    for (std::size_t i = 0; i < arr.size(); ++i) {
        std::cout << arr[i] << '\n';
    }
}
```

Again, note that even when the initialization of and iteration over are happening in different translation units the same variable `std::array<int, 10>` of global scope is still used.

### Variable Templates for Data Members

A useful application of variable templates is to define variables that represent members of class templates. For example, if a class template is defined as follows:

```cpp
template<typename T>
class MyClass {
public:
    static constexpr int max = 1000;
};
```

which allows you to define different values for different specializations of `MyClass`, then you can define

```cpp
template<typename T>
int myMax = MyClass<T>::max;
```

so that application programmers can just write

```cpp
auto i = myMax<std::string>;
```

instead of

```cpp
auto i = MyClass<std::string>::max;
```

This means, for a standard class such as

```cpp
namespace std {
    template<typename T> class numeric_limits {
    public:
        static constexpr bool is_signed = false;
        ...
    };
}
```

you can define

```cpp
template<typename T>
constexpr bool is_signed = std::numeric_limits<T>::is_signed;
```

to be able to write

`is_signed<char>`

instead of

`std::numeric_limits<char>::is_signed`

### Type Traits Suite

Since C++17, the standard library uses the technique of variable templates to define shorthand for all type traits in the standard library that yield a (Boolean) value. For example, to be able to write

```cpp
std::is_const_v       // since C++17
```

## 5.7 TEMPLATE TEMPLATE PARAMETERS

It can be useful to pass a template parameter itself to a class template. Again, our stack class template can be used as an example.

To use a different internal container for stacks, the application programmer has to specify the element type twice. Thus, to specify the type of the internal container, you have to pass the type of the container and the type of its elements again:

```cpp
Stack<int, std::vector<int>> vstack;    // integer stack that uses a vector
```

Using template template parameters allows you to declare the `Stack` class template by specifying the type of the container without repeating the type of its elements:

```cpp
Stack<int, vector> vstack;    // integer stack that uses a vector
```

To do this, you must specify the second template parameter as a template template parameter. In principle, this looks as follows:

```cpp
template<typename T,
         template<typename Elem> class Cont = std::deque>
class Stack {
private:
    Cont<T> elems;             // elements
public:
    void push(T const&);       // push element
    void pop();                // pop element
    T const& top() const;      // return top element
    bool empty() const {       // return whether the
        return elems.empty();
    }
};
```

The difference is that the second template parameter is declared as being a class template:

```cpp
template<typename T, template<typename Elem> class Cont
         = std::deque>
class Stack {
    Cont<T> elems;             // OK
};
```

The default value has changed from `std::deque<T>` to `std::deque`.

```cpp
Cont<T> elems;
```

This use of the first template parameter for the instantiation of the second template parameter is particular to this example. In general, you can instantiate a template parameter from any type you provide in a class template.

As usual, instead of `typename` you could use the keyword `class` for template parameters. Before C++11, it could only be introduced by the name of a class template.

```cpp
template<typename T,
         template<class Elem> class Cont = std::deque>
class Stack {                          // OK
    ...
};
```

Since C++11, we can also substitute `Cont` with the name of an alias template, but it wasn't until C++17 that a corresponding change was made to permit the use of the keyword `typename` instead of `class` to declare a template parameter:

```cpp
template<typename T,
         template<typename Elem> typename Cont =
         std::deque>
class Stack {                          // ERROR before C++17
    ...
};
```

Because the template parameter of the template template parameter is not used, it is customary to omit its name (unless it provides useful documentation):

```cpp
template<template<typename> class Cont = std::deque>
class Stack {
    // ...
};
```

Member functions must be modified accordingly. Thus, you have to specify the second template parameter at the template template parameter. The same applies to the implementation of the member function. The `push()` member function, for example, is implemented as follows:

```cpp
template<typename T, template<typename> class Cont>
void Stack<T, Cont>::push (const T& elem)
{
    elems.push_back(elem);    // append copy of passed
}
```

Notice that while template template parameters are placeholders for class or alias templates, there is no corresponding placeholder for function or variable templates.

### Template Template Argument Matching

If you try to use the new version of `Stack`, you may get an error message saying that the default value `std::deque` is not compatible with the template parameter `Cont`. The problem is that prior to C++17 a template argument had to be a template with parameters that exactly match the parameters of the template template parameter it substitutes, with some exceptions related to variadic template parameters (see Section 12.3.4 on page 107). Default template arguments of template template arguments are not considered, so that a match couldn't be achieved by leaving out arguments that have default values (in C++17, default arguments are considered).

The pre-C++17 problem in this example is that the `std::deque` of the standard library has more than one parameter. The second parameter of `std::deque` allows an allocator (as a default value), but prior to C++17 this was not considered when matching `std::deque` to the `Cont` parameter.

There is a workaround, however. We can rewrite the class declaration so that the `Cont` parameter expects containers with two template parameters:

```cpp
template<typename T,
         template<typename, typename> class Cont = std::deque>
class Stack {
private:
    Cont<T> elems;        // elements

public:
    void push (T const&); // push element
    void pop ();          // pop element
    T const& top() const; // return top element
};
```

The final version of our `Stack` template (including member templates for assignments of stacks of different element types) now looks as follows:

```cpp
#include <deque>
#include <cassert>
#include <memory>

template<typename T,
         template<typename T, typename = std::allocator<T>>
                   class Cont = std::deque>
class Stack {
private:
    Cont<T> elems;        // elements

public:
    void push (T const&); // push element
    void pop ();          // pop element
    T const& top() const; // return top element
    // ...
};
```

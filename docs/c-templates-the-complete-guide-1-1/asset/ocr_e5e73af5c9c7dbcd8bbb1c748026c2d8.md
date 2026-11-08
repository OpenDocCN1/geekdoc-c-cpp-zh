```
```cpp
class Collection {
public:
    template<typename T>             // an in-class member
    class Node {
        ...
    };

    template<typename T>             // an in-class (and the...
    T* alloc() {                     // member function tem...
        ...
    }

    template<typename T>             // a member variable
    static T zero = 0;

    template<typename T>             // a member alias tem...
    using NodeType = Node<T>;
};
```
```

Note that in C++17, variables—including static data members—and variable templates can be “inline,” which means that their definition can be repeated across translation units. This is redundant for variable templates, which can always be defined in multiple translation units. Unlike member functions, however, a static data member being defined in its enclosing class does not make it inline: The keyword `inline` must be specified on it.

Finally, the following code demonstrates how member templates that are not alias templates can be defined out-of-class:

Click here to view code image

```
```cpp
template<typename T>             // a namespace scope
class List {
public:
    List() = default;              // because a template

    template<typename T>           // another member class
    class Handler                  // without its definition
    ...

    template<typename T>           // a member function
    List (List<T> const&);          // (constructor)

    template<typename T>           // a member variable
    static T zero;
};

template<typename T>               // out-of-class member

template<typename T>               // out-of-class member
class List<T>::Handler {
    ...
};

template<typename T>               // out-of-class member

template<typename T>               // out-of-class member
List<T>::List (List<T> const& b)
{
    ...
}
```
```
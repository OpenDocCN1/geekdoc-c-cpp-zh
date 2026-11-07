```
```cpp
}
```
```

The problem is that the elements in a `std::vector<bool>` are not objects of type bool; they are single bits. The way this is implemented is that for `std::vector<bool>` the type of a reference to an element is *not* a reference to the element type. The implementation of class `std::vector<bool>` is a partial specialization of the implementation of the primary template `std::vector<T>` where references to elements are objects of a proxy class that you can use like a reference:

```
```cpp
namespace std {
    template<...>
      class vector<bool, ...> {
      public:
        ...
        class reference {
          ...
        };
        ...
      };
}
```
```

A value of this class `std::vector<bool>::reference` is returned when dereferencing an iterator. Therefore, in the expansion of the range-based for loop, the statement

```
```cpp
auto& elem = *pos;
```
```

tries to bind a non-const lvalue reference to a temporary object (prvalue), which is not allowed. However, there is a solution to the problem: use a universal reference when calling the range-based `for` loop instead:

```
```cpp
template<typename Coll, typename T>
void assign(Coll& coll, const T& value) {
    for (auto&& elem : coll) {  // note: universal reference support proxy element types
        elem = value;
    }
}
```
```

Because a universal reference can bind to any object of any value category (even to a prvalue), using this generic code with `vector<bool>` now compiles:

```
```cpp
std::vector<bool> collB{false, true, false};
...
assign(collB, true);  // OK (universal reference used to bind to an element)
```
```

We have thus found another reason to use non-forwarding universal references: they bind to reference types that are not implemented as references. Or, more generally: they allow us to bind to non-const objects provided as proxy types to manipulate objects.
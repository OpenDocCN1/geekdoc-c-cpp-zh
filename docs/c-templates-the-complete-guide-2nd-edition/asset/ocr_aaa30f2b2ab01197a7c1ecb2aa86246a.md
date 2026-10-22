```
```cpp
template<typename T,
         template<typename Elem,
                  typename Alloc = std::allocator<Elem>>
                  class Cont = std::deque>
class Stack {
private:
    Cont<T> elems;        // elements
    ...
};
```
```
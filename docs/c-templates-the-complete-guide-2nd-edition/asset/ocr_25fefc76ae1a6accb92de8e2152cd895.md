```
```cpp
template<typename VHead, typename... VTail>
Tuple(Tuple<VHead, VTail...> const& other)
  : head(other.getHead()), tail(other.getTail()) { }
```
```
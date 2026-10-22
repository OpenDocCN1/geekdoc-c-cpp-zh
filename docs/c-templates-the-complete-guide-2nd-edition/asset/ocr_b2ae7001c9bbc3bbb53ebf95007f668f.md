```
```cpp
template<int I, typename... T> class V {
    V* a;          // OK: same as "V<I, T...>* a;"
    V<0, void> b;  // OK
};
```
```
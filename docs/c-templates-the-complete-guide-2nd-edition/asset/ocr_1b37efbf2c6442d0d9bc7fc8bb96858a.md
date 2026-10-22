```
```cpp
template<int I, bool B>
class C;
...
C<sizeof(int) + 4, sizeof(int)==4> c;
```
```
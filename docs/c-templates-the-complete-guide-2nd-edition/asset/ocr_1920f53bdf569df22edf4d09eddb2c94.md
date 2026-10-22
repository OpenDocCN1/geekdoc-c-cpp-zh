```
```cpp
void f();
template<typename> void f();
namespace N {
  class C {
    friend int f();              // OK
    friend int f<>();            // ERROR: return type conflict
  };
}
```
```
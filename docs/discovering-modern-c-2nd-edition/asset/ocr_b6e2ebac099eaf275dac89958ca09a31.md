```
```cpp
tray1 a1, c1,
    b1{std::move(a1)}; // Compiles but uses copy constructor
c1 = std::move(b1);   // Compiles but uses copy assignment

tray2 a2, c2,
    b2{std::move(a2)}; // Error: deleted move constructor
c2 = std::move(b2);   // Error: deleted move assignment
```
```
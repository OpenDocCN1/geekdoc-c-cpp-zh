```
class tray1
{
public:
    tray1(const tray1&) = default;
    // tray1(tray1&&) noexcept // not generated
    tray1& operator=(const tray1&) = default;
    // tray1& operator=(tray1&&) noexcept // not generated
};
// ..
```

versus:

Click here to view code image

```
class tray2
{
public:
    tray2(const tray2&) = default;
    tray2(tray2&&) noexcept = delete;
    tray2& operator=(const tray2&) = default;
    tray2& operator=(tray2&&) noexcept = delete;
};
// ..
```

In both cases, the copy operations have default behavior while the move operations are absent. We could expect them to behave equally. But they do not when an rvalue is passed:

Click here to view code image

```
tray1 a1, c1,
    b1{std::move(a1)}; // Compiles but uses copy
constructor
c1 = std::move(b1); // Compiles but uses copy
assignment

tray2 a2, c2,
    b2{std::move(a2)}; // Error: deleted move constructor
c2= std::move(b2); // Error: deleted move assignment
```

A class with implicitly deleted move operations like tray1 can handle rvalues. However, the values are actually not moved but copied. The reason is that rvalue references can be implicitly converted to constant lvalue references so that the according copy operations are the best matches. In contrast an explicitly deleted move operation like in tray2 is the best match for an rvalue and the move operation is forbidden.
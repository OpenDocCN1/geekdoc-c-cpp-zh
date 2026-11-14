The implicit generation of one copy operation in the presence of its counterpart is branded as deprecated in C++11 and C++14 but willingly provided by compilers (usually without protest):

```
```cpp
class tray
{
public:
    tray(const tray&) = default; // considered user-defined
    // tray& operator=(const tray&) = default; // deprecated
    // ...
};
```
```

Likewise, when the destructor is user-defined, the generation of copy operations is deprecated but still supported.

# A.5.2.6 Rule 5: How Copy Operations Are Generated

The copy operations take constant references as arguments, under normal conditions. It is allowed to implement copy operations with mutable references, and we discuss this here for completeness' sake rather than for practical relevance (and as kind of a warning example). If any of a class's members requires a mutable reference in a copy operation, the generated operation also requires a mutable reference:

```
```cpp
struct mutable_copy
{
    mutable_copy() = default;
    mutable_copy(mutable_copy& ) {}
    mutable_copy(mutable_copy&& ) = default;
    mutable_copy& operator=(const mutable_copy& ) = default;
    mutable_copy& operator=(mutable_copy&& ) = default;
};
```
```

```
```cpp
class tray
{
public:
    // tray(tray&) = default;
    // tray(tray&&) = default;
    // tray& operator=(const tray&) = default;
    // tray& operator=(tray&&) = default;
    mutable_copy m;
    // ...
};
```
```

The class mutable_copy only accepts mutable references in its copy constructor. Therefore, that of tray also requires a mutable reference. In the case that the compiler generates it, it will be non-const. An explicitly declared copy constructor with a const reference:

```
```cpp
class tray
{
    tray(const tray&) = default;
```
```
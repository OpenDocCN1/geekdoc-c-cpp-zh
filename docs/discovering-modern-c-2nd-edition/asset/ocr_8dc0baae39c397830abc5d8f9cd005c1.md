```
```cpp
class tray
{
  public:
    tray(const tray&) = default;
    // tray(tray&&) = delete; // implicit
    // tray& operator=(tray&&) noexcept = delete; // implicit
    // ...
};
```
```
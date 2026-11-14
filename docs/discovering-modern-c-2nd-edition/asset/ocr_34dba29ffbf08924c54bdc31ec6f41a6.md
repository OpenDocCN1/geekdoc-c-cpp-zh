```
class tray
{
public:
    tray(const tray&) = default;
    // move constructor actually copies
    tray(tray&& that) noexcept : tray(that) {}
    tray& operator=(const tray&) = default;
    // move assignment actually copies
    tray& operator=(tray&& that) noexcept { return *this = that; }
};
// ...
```
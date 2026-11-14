```
class tray
{
public:
// tray(const tray&) = delete; // implied
tray(tray&&) noexcept = default; // considered user-defined
// tray& operator=(const tray&) = delete; // implied
// ...
};
```
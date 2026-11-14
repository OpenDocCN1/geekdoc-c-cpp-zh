```
class move_only
{
public:
    move_only() = default;
    move_only(const move_only&) = delete;
    move_only(move_only&&) noexcept = default;
    move_only& operator=(const move_only&) = delete;
    move_only& operator=(move_only&&) noexcept = default;
    ~move_only() = default;
    // ...
};
```
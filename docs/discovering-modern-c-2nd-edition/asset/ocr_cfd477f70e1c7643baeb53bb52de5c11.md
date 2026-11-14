```
template <typename ...Args>
void print4(ostream& os, const Args& ...args)
{
    auto dummy={(os << args << ", ", 0)...};
    os << '\n';
}
```
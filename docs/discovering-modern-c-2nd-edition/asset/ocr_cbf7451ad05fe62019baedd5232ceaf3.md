```
template <typename ...Args>
void print1(ostream& os, const Args& ...args)
{
    (os << args << ", ")...; // Error: Can't expand here
    os << '\n';
}
```
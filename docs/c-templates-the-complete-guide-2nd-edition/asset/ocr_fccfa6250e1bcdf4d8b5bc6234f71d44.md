```
template<typename T> auto f(T p) {
    return p->m;
}

int f(...);

template<typename T> auto g(T p) -> decltype(f(p));

int main()
{
    g(42);
}
```
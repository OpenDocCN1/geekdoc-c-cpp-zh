```
// let f() perfect forward argument val to g():
template<typename T>
void f (T&& val) {
    g(std::forward<T>(val));    // call the right g() for any passed argument val
}

int main()
{
    X v;                // create variable
    X const c;          // create constant

    f(v);               // f() for variable calls f(X&)  => calls g(X&)
    f(c);               // f() for constant calls f(X const&)  => calls g(X const&)
    f(X());             // f() for temporary calls f(X&&)  => calls g(X&&)
    f(std::move(v));    // f() for move-enabled variable calls f(X&&)  => calls g(X&&)
}
```
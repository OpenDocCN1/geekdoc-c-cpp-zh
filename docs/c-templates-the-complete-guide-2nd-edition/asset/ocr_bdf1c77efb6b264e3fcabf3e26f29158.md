```
void f (X& val) {
    g(val);        // val is non-const lvalue => calls g(X&)
}
void f (X const& val) {
    g(val);        // val is const lvalue  => calls g(X const&)
}
void f (X&& val) {
    g(std::move(val));  // val is non-const lvalue => needs std::move() to call g(X&&)
}
```
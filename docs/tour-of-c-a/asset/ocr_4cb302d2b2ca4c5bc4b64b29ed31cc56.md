```
void f1()\n{
    auto p = make_unique<int>(2);
    auto q = p;             // error: we can't copy a unique_ptr
    auto q = move(p);       // p now holds nullptr
    // ...
}
```
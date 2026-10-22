```
template<typename T>
T foo(T*)
{
}

void* vp = nullptr;
foo(vp);            // OK: deduces void foo(void*)
```
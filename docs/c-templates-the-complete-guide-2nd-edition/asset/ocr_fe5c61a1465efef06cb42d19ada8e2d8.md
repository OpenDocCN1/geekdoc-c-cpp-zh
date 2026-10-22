```
void f() { }

template<int x> void nondependentCall()
{
    f(x);    // x is value-dependent, so f() is nondependent;
             // this call will never succeed
}
```
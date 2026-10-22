```
```cpp
template<typename T>
void ignore(T const&)
{
}

template<typename T>
void shell (T const& env)
{
    class ShallowChecks
    {
        void deref(typename T::Index ptr) {
            ignore(*ptr);
        }
    };
    typename T::Index i;
    middle(i);
}
```
```
```
template<Number... T>
int sum(T... v)
{
    return (v + ... + 0); // Il add all elements of v starting with 0
}
```
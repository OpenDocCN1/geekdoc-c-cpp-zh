```
template<typename T, unsigned N>
T* begin(T (&array)[N])
{
    return array;
}

template<typename Container>
typename Container::iterator begin(Container& c)
{
    return c.begin();
}

int main()
{
    std::vector<int> v;
    int a[10];

    ::begin(v);  // OK: only container begin() matches, because the first deduction fails
    ::begin(a);  // OK: only array begin() matches, because the second substitution fails
}
```
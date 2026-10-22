```
template<typename T> T default_value()
{
    return T{};
}

int main()
{
    return default_value<int>();
}
```
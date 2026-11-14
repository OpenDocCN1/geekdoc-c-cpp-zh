```
constexpr bool is_prime(int i)
{
    if (i == 1)
        return false;
    if (i % 2 == 0)
        return i == 2;
    for (int j= 3; j < i; j+= 2)
        if (i % j == 0)
            return false;
    return true;
}
```
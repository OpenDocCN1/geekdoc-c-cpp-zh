```
constexpr bool is_prime(int i)
{
    if (i == 1)
        return false;
    if (i % 2 == 0)
        return i == 2;
    int max_check= square_root(i) + 1;
    for (int j = 3; j < max_check; j+= 2)
        if (i % j == 0)
            return false;
    return true;
}
```

With this example we have seen how the performance of compile-time evaluation improved. Around 2006, this function took around 18s for a prime number close to 1 million and about one minute for a prime number close to 10 million. With `constexpr` on g++-10 the test of a prime number near 1 billion increased the compile time by ≈ 0.02s.

=> c++11/is_prime.cpp

At the end, we like taking the challenge to implement this (well, the first version of it) with the restricted `constexpr` in C++11:

Click here to view code image

```
constexpr bool is_prime_aux(int i, int div)
{
    return div >= i ? true :
           (i % div == 0 ? false : is_prime_aux(i, div + 2));
}

constexpr bool is_prime(int i)
{
    return i == 1 ? false :
           (i % 2 == 0 ? i == 2 : is_prime_aux(i, 3));
}
```

Here we need two functions: one for the special cases and one for checking the divisibility by odd numbers from 3.

**Backward compatibility:** Before `constexpr` was introduced, compile-time calculations were realized with template _Meta-Functions_. They are harder to implement and before C++20 they were also more limited in their applicability (neither `float` nor user types). If you cannot use C++11
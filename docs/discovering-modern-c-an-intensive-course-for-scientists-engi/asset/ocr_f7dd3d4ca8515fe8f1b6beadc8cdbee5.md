# 5.1.3 Primeness

We have already mentioned that prime numbers were the topic of the first serious metaprogram, although not compilable. Now we want to demonstrate that we can compute them in (compilable) modern C++. More precisely, we will implement a function that tells us at compile time whether a given number is prime. You may ask: “Why on earth do I need this information during compilation?” Fair question. Actually, the author used this compile-time function once in his research for categorizing cyclic groups with semantic concepts (§8.5). When the size of the group is a prime number, it is a field, otherwise a ring. An experimental compiler (ConceptGCC [21]) enabled such algebraic concepts in C++, and their model declarations contained the compile-time check for primeness (unfortunately before concepts was available).

```
=> c++14/is_prime.cpp
```

Our algorithmic approach is that 1 is not prime, even numbers are not prime except 2, and for all other numbers we check that they are not divisible by any odd number larger than 1 and smaller than itself:

```
constexpr bool is_prime(int i)
{
    if (i == 1)
        return false;
    if (i % 2 == 0)
        return i == 2;
    for (int j = 3; j < i; j+= 2)
        if (i % j == 0)
            return false;
    return true;
}
```

Actually, we only need to test the divisibility by odd numbers smaller than the square root of the parameter i:

```
constexpr bool is_prime(int i)
{
    if (i == 1)
        return false;
    if (i % 2 == 0)
        return i == 2;
    int max_check = static_cast<int>(sqrt(i)) + 1;
    for (int j = 3; j < max_check; j+= 2)
        if (i % j == 0)
            return false;
    return true;
}
```

Unfortunately, this version only works with standard libraries where sqrt is a constexpr (>= 4.7-4.9 as before). Otherwise we have to provide our own constexpr implementation. For instance, we can use the fixed-point algorithm from Section 4.3.1:
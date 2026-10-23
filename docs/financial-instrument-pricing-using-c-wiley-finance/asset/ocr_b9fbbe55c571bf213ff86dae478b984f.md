Other operators are:

```
ratio_not_equal
ratio_less
ratio_less_equal
ratio_greater
ratio_greater_equal.
```

Finally, the standard library supports SI (International System of Units) ratios (all in the namespace std):

```
typedef ratio<1, 1000000000000000000> atto;
typedef ratio<1, 1000000000000000> femto;
typedef ratio<1, 1000000000000> pico;
typedef ratio<1, 1000000000> nano;
typedef ratio<1, 1000000> micro;
typedef ratio<1, 1000> milli;
typedef ratio<1, 100> centi;
typedef ratio<1, 10> deci;
typedef ratio<10, 1> deca;
typedef ratio<100, 1> hecto;
typedef ratio<1000, 1> kilo;
typedef ratio<1000000, 1> mega;
typedef ratio<1000000000, 1> giga;
typedef ratio<1000000000000, 1> tera;
typedef ratio<1000000000000000, 1> peta;
typedef ratio<1000000000000000000, 1> exa;
```

Some examples are:

```
template <std::intmax_t Num, std::intmax_t Den>
    void print(const std::ratio<Num, Den>& r)
{
    std::cout << r.num << "/" << r.den << '\n';
}

// SI units
std::kilo myKilo; print(myKilo);        // 1000/1
std::milli myMilli; print(myMilli);     // 1/1000

std::nano myNano; print(myNano);        // 1/1'000'000'000
std::giga myGiga; print(myGiga);        // 1'000'000'000/1
```

The chrono library uses std::ratio<>.
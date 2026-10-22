```
template<typename T, typename U>
struct Doublify {
};

template<int N>
struct Trouble {
    using LongType = Doublify<typename Trouble<N-1>::LongType,
        typename Trouble<N-1>::LongType>;
};

template<>
struct Trouble<0> {
    using LongType = double;
};

Trouble<10>::LongType ouch;
```
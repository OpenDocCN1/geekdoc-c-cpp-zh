```
template<typename... Elements>
class Tuple; // primary template

template<typename T1>
class Tuple<T>; // one-element tuple

template<typename T1, typename T2, typename... Rest>
class Tuple<T1, T2, Rest...>; // tuple with two or more elements
```
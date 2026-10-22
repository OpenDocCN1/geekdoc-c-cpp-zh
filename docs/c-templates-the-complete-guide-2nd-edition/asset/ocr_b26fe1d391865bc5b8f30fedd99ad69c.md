```
template<typename T1, typename T2>
class Pair {
    T1 first;
    T2 second;
public:
    Pair(Pair&& other)
        : first(std::forward<T1>(other.first)),
          second(std::forward<T2>(other.second)) {
    }
};
```
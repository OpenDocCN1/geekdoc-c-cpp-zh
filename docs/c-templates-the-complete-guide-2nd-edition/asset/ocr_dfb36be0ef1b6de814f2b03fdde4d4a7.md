```
template<int& Counter>
struct LocalIncrement {
    LocalIncrement() { Counter = Counter + 1; }  // OK: reference to an integer
    ~LocalIncrement() { Counter = Counter - 1; }
};
```
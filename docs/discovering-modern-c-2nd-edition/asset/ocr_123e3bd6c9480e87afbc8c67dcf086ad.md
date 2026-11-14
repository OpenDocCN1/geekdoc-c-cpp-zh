```
template <typename Value>
struct power {
    Value operator()(Value x, Value y) const { return pow(x, y); }
};

functions.push_back(power{}); // Error
```
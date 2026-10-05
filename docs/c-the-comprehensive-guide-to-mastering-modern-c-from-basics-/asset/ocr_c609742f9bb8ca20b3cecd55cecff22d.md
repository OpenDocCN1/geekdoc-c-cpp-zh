Here you see with int val such a nontype parameter,
which can be used like a constant. However, this
ontype parameter must be an integer type. In practice,
this nontype parameter is often given a default value,
which is used if no value is specified for this parameter
during instantiation:

```
template<typename T, int val=10> // with default value
// ...
```

I want to create a simplified version of the fixed array
std::array to demonstrate the nontype parameter. Here
is the code, with an explanation following:

```
// https://github.com/rz/E89bav3rE
#include <iostream>
template <typename T, size_t n=1> // Nontype parameter with default
value
class FixedArray {
    T data_[n] = {}; // Using nontype parameter
public:
    T& operator[](size_t index) { return data_[index]; }
    static const size_t size() { return n; }
    void print(std::ostream &os) const {
        for(auto it : data_) {
            os << it << '\n';
        }
    }
};
int main() {
    FixedArray<int,10> vals; // n = 10
    for(size_t idx=0; idx < vals.size(); ++idx) {
        vals[idx] = idx+idx;
    }
    vals.print(std::cout); // Output: 0 2 4 6 8 10 12 14 16 18
    FixedArray<double> dvals; // Default parameter for n
    std::cout << dvals.size() << '\n'; // Output: 1
}
```
```
const_iterator cbegin() const;
const_iterator cend() const;
};
```

If your container is, for example, a const parameter of a function, you can only get back a const_iterator. If the container is mutable, you should decide which iterator type you need.

Do you not always have to type "std::vector<std::string>:::const_iterator" when programming a loop? You do not have to. auto helps you here the compiler uses it to calculate the correct type:

```
// https://godbolt.org/dxb98Wzo
#include <iostream>
#include <vector>
using std::vector;
vector<int> createData(size_t sz) {
    return vector<int>(sz); // sz null
}
void fibonacci(vector<int> &data) {
    for(auto it = begin(data)+2; it != end(data); ++it) { // iterator it
        *it = *(it-1) + *(it-2);
    }
}
::ostream& show(std::ostream &os, const vector<int> &data) {
    for(auto it=begin(data); it != end(data); ++it) // const_iterator
        os << *it << " ";n    return os;
}
int main() {
    vector<int> data = createData(10);
    data[0] = i;
    data[1] = 1;
    fibonacci(data);
    show(std::cout, data) << "\n";
}
```

# Listing 24.8 For "const" objects, "begin()" and "end()" return a "const_iterator".
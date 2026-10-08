```
class Vector {
public:
    Vector(); // default initialize to "empty"; that is, to no elements
    Vector(std::initializer_list<double>); // initialize with a list of doubles
    // ...
    void push_back(double); // add element at end, increasing the size by one
    // ...
};
```
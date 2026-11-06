```
```cpp
41    if (size != right.size) {
42        delete[] ptr; // release space
43        size = right.size; // resize this object
44        ptr = new int[size]; // create space for Array copy
45    }

47    for (size_t i{0}; i < size; ++i) {
48        ptr[i] = right.ptr[i]; // copy array into object
49    }
50}

52    return *this; // enables x = y = z, for example
53}

55    // determine if two Arrays are equal and
56    // return true, otherwise return false
57    bool Array::operator==(const Array& right) const {
58        if (size != right.size) {
59            return false; // arrays of different number of elements
60        }

62        for (size_t i{0}; i < size; ++i) {
63            if (ptr[i] != right.ptr[i]) {
64                return false; // Array contents are not equal
65            }
66        }

68        return true; // Arrays are equal
69    }

71    // overloaded subscript operator for non-const Arrays;
72    // reference return creates a modifiable lValue
73    int& Array::operator[](int subscript) {
74        // check for subscript out-of-range error
75        if (subscript < 0 || subscript >= size) {
76            throw out_of_range{"Subscript out of range"};
77        }

79        return ptr[subscript]; // reference return
80    }
```
```
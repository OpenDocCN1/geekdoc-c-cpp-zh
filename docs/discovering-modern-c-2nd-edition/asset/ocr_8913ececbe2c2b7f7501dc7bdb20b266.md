```
template <typename T> class vector_sum; // forward declaration
template <typename T>
class vector
{ // ...
    vector& operator=(const vector_sum<T>& that)
    {
        check_size(size(that));
        for (int i = 0; i < my_size; ++i)
            data[i] = that[i];
        return *this;
    }
};
```
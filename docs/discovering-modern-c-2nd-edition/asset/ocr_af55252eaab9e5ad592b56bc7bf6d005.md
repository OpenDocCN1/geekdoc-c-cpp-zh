```
```cpp
template <typename T>
class vector
{
    template <typename Src>
    vector& operator=(const Src& that)
    {
        check_size(size(that));
        unsigned s = my_size, sb = s / 4 * 4;

        for (unsigned i = 0; i < sb; i+= 4)
            assign<0, 4>::eval(*this, that, i);

        for (unsigned i = sb; i < s; ++i)
            data[i]= that[i];
        return *this;
    }
};
};
```
```
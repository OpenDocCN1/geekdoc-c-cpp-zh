```
size_t _size;    // number of elements
size_t _capa;    // capacity
public:
    void push_back(const T& t) {
        if (_capa == _size) {
            reserve((_capa+1)*2);
        }
        ATR::construct(_alloc, _elems+_size, t);  // calls placement new
        ++_size;
    }

    T& operator[] (size_t i){
        return std::launder(_elems)[i];  // OOPS, still UB
    }
    ...
};
```

the call of launder() in operator[] does not help because the pointer might be a smart pointer (i.e., a class type) and for them, launder() has no effect.¹

Also trying
std::launder(this)->_elems[i];

does not work because launder() works only for pointers to objects for which the lifetime has ended.²

Thus, std::launder() does not solve the problem of avoiding undefined behavior in allocator-based containers if you have elements with constant/reference members. It appears that a general core fix is necessary (see my paper http://wg21.link/p0532).

# 32.4 Afternotes

std::launder() was introduced as a result of a national body comment for C++14 (see http://wg21.link/n3903) and was first discussed as core working group issue 1776 (see http://wg21.link/cwg1776). As a solution, it was first proposed by Richard Smith and Hubert Tong in http://wg21.link/n4303. The finally accepted wording was formulated by Richard Smith in http://wg21.link/p0137r1.
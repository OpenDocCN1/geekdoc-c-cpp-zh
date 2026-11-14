```
using value_type= std::common_type_t<typename
V1::value_type,
typename V2::value_type>;
value_type operator[](int i) const { return v1[i] +
v2[i]; }
```

If our class `vector_sum` does not need the explicit declaration of a `value_type`, we can use `decltype(auto)` in C++14 as a return type and leave the type deduction entirely to the compiler. In contrast, trailing return types do not work when the template is instantiated with `vector_sum` itself as this creates a dependency on itself. To assign different kinds of expressions to a vector class, we should also generalize the assignment operator:

Click here to view code image

```
template <typename T>
class vector
{
public:
    template <typename Src>
    vector& operator=(const Src& that)
    {
        check_size(size(that));
        for (int i=0; i < my_size; ++i)
            data[i] = that[i];
        return *this;
    }
};
```

This assignment operator accepts every type except `vector<T>` for which we need a dedicated copy-assignment operator. To avoid code redundancy, we could implement a method that performs the actual copy and is called from both the general and the copy assignment.

# C++11 5.3.4 Copy Before It's Stale

A problem with the generic expression templates just introduced is the validity of references when the expressions grow larger. At some point, we end up with a stale reference to a sub-expression's ET object that is already destroyed.
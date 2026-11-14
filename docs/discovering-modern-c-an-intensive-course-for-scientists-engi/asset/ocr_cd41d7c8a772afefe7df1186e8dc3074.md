```
template <typename Target, typename Source>
struct fsize_assign<Target, Source, 0>
{
    void operator()(Target& tar, const Source& src)
    {
        std::cout << "assign entry " << 0 << '\n';
        tar[0] = src[0];
    }
};
```

The printouts will show us the execution. To save ourselves from explicitly instantiating the argument types, we parameterize the operator() instead of the class:

```
template <int N>
struct fsize_assign
{
    template <typename Target, typename Source>
    void operator()(Target& tar, const Source& src)
    {
        fsize_assign<N-1>()(tar, src);
        std::cout << "assign entry " << N << '\n';
        tar[N] = src[N];
    }
};
```

```
template <>
struct fsize_assign<0>
{
    template <typename Target, typename Source>
    void operator()(Target& tar, const Source& src)
    {
        std::cout << "assign entry " << 0 << '\n';
        tar[0] = src[0];
    }
};
```

Then the vector types can be deduced by the compiler when the operator is called. Instead of a loop implementation, we call the recursive assignment functor in the operator:

```
template <typename T, int Size>
class fsize_vector
{
    static_assert(my_size > 0, "Vector must be larger than 0.");
    self& operator=(const self& that)
    {
        fsize_assign<my_size-1>()(*this, that);
        return *this;
    }
}
```
```
template <size_t N>
class vector_f {
public:
    vector_f();
    vector_f(std::initializer_list<float> init);
    float operator[](size_t i) const; // read-only accessor
    float& operator[](size_t i); // read-write accessor
    size_t const size(); // extract the size parameter
private:
    std::array<float, N> data;
};
```

We want to be able to add vector_f objects together. This means we will need an addition operator function template:

Click here to view code image

```
template <size_t N>
vector_f<N> operator+(vector_f<N> const& u, vector_f<N> const& v) {
    vector_f<N> sum;
    for (size_t i = 0; i < N; i++) {
        sum[i] = u[i] + v[i];
    }
    return sum;
}
```

No rocket science here. It’s a raw loop, but we want to highlight something: the code creates the return value, populates it, and returns it. The compiler can do some loop unrolling for small values of N. We cannot initialize the
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
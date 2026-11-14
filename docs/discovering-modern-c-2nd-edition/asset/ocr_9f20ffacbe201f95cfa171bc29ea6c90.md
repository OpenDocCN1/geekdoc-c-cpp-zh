```
class some_matrix; // Forward declaration

class simple_bracket_proxy
{
public:
    simple_bracket_proxy(some_matrix& A, size_t r)
        : A(A), r(r) {}

    double& operator[](size_t c){ return A(r, c); } // Error
private:
    some_matrix& A;
    size_t r;
};

class some_matrix
{
    // ...
    double& operator()(size_t r, size_t c) { ... }

    simple_bracket_proxy operator[](size_t r)
    {
        return simple_bracket_proxy(*this, r);
    }
};
```
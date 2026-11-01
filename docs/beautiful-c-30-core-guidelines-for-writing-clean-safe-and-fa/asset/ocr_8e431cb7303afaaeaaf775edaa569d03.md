```
E1 const& u;
E2 const& v;

public:
    vector_sum(E1 const& u, E2 const& v);
    float operator[](size_t i) const { return u[i] + v[i]; } //(2)
    size_t size() const { return v.size(); }
};
```

```
template <typename E1, typename E2>
vector_sum<E1, E2> operator+(vector_expression<E1> const& u,
const& u,
                    vector_expression<E2>
const& v) {
    return vector_sum<E1, E2>(*static_cast<E1 const*>(&u),
const*>(&u),
                    *static_cast<E2
const*>(&v));
}
```

That is everything required for addition. The expression

a + b + c

is now no longer of the type vector_f<3>, but of the type

Click here to view code image

vector_sum<vector_sum<vector_f<3>, vector_f<3>>>

When this expression is assigned to a vector_f<3> object, the constructor that takes a vector_expression is invoked, which assigns the expression elements to the data ele-ments (1). The bracket operator for
mechanism, we now go directly to the general version working for arbitrary vector types and views thereof:

Click here to view code image

```
```cpp
template <typename V1, typename V2>
inline vector_sum<V1, V2> operator+(const V1& x, const V2& y)
{
    return {x, y};
}
```
```

We now need an expression class with arbitrary arguments:

Click here to view code image

```
```cpp
template <typename V1, typename V2>
class vector_sum
{
public:
    vector_sum(const V1& v1, const V2& v2) : v1{v1}, v2{v2}
    {}

    ??? operator[](int i) const { return v1[i] + v2[i]; }

private:
    const V1& v1;
    const V2& v2;
};
```
```

This is rather straightforward. The only issue is what type to return in operator[]. For this we must define value_type in each class (an external type trait would be more flexible but we want to keep it as simple as possible here). In vector_sum, we could take the value_type of the first argument, which can itself be taken from another class. This is an acceptable solution as long as the scalar types are identical in the entire application. However, we have seen in Section 3.11 that we can get completely absurd results with mixed arguments when we do not pay attention to the result types. To be prepared for mixed arithmetic, we take the common_type_t of the arguments' value types:

Click here to view code image

```
```cpp
template <typename V1, typename V2>
class vector_sum
{
    // ...
}
```
```
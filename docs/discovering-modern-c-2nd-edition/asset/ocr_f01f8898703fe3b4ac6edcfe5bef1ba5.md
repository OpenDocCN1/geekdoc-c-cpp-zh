The first statement can be quite verbose when `expr` is long and everything we add to it needs to be added twice in this statement. And for every modification we must pay attention that the two expressions are still identical.

=> c++14/value_range_vector.cpp

The preservation of qualifiers is also important in automatic `return` types. As an example we introduce a view on vectors that tests whether the values are in a given range.

The view will access an element of the viewed vector with `operator[]` and return it after the range test with exactly the same qualifiers. Obviously a job for `decltype(auto)`. Our example implementation of this view only contains a constructor and the access operator:

Click here to view code image

```
template <typename Vector>
class value_range_vector
{
    using value_type= typename Vector::value_type;
    using size_type= typename Vector::size_type;
    public:
        value_range_vector(Vector& vref , value_type minv ,
        value_type maxv)
        : vref(vref), minv(minv), maxv(maxv)
        {
        }

        decltype(auto) operator[](size_type i)
        {
            decltype(auto) value= vref[i];
            if (value < minv) throw too_small{};
            if (value > maxv) throw too_large{};
            return value;
        }

    private:
        Vector&
            vref;
        value_type minv, maxv;
};

```

Our access operator caches the element from `vref` for the range checks before it is returned. Both the type of the temporary and the `return` type are deduced with `decltype(auto)`. To see that vector elements are returned with
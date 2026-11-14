```
```cpp
template <std::random_access_iterator Iter, typename Value,
          typename Op>
Value accumulate(Iter first, Iter last, Value init, Op op)
    requires Accumatable<Iter, Value, Op>
        && CommutativeMonoid<Op, Value>
{
    auto t1= identity(op, *first), t2= t1, t3= t1;
    auto size= last - first;
    auto bsize= size / 4 + 4;
    for (Iter blast= first + bsize; first != blast; first+= 4) {
        init= op(init, *first);
        t1= op(t1, *(first+1));
        t2= op(t2, *(first+2));
        t3= op(t3, *(first+3));
    }
    for (; first != last; ++first)
        init= op(init, *first);
    return op(op(init, t1), op(t2, t3));
}
```
```
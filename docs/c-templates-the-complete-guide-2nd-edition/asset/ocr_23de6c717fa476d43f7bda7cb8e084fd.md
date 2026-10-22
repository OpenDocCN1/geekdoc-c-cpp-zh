```
```cpp
template<typename T, typename R1, typename R2>
Array<T, A_Mult<T,R1,R2>>
operator* (Array<T,R1> const& a, Array<T,R2> const& b) {
    return Array<T,A_Mult<T,R1,R2>>
        (A_Mult<T,R1,R2>(a.rep(), b.rep()));
}
```
```
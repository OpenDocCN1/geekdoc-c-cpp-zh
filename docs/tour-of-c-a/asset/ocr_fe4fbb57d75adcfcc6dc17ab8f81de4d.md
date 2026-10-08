```
template<typename T, typename U = T>
concept Number =
    requires(T x, U y) { // Something with arithmetic operations and a zero
    x+y; x-y; x*y; x/y;
    x+=y; x-=y; x*=y; x/=y;
    x=x; // copy
    x=0;
};
```
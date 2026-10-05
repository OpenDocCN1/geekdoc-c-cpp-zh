You saw in Section 23.1.3, in the “C++20: Abbreviated Function Template” box, that this use of auto has also been applicable to functions since C++20. And also introduced with C++20 is the ability to write a true template lambda:

```
// https://godbolt.org/z/nenW8aM81
auto min2 = [<typename T>(const T &a, const T &b) {
    return a < b ? a : b;
};
auto min3 = [<typename T>(const T &a, const T &b, const T &c) {
    return min2(a, min2(b,c));
};
```

With this feature, you enforce that the parameters must have the same type.
# Modern C++: [[no_unique_address]] (C++20)

The attribute [[no_unique_address]] states that a data member of a class need not have a unique address. Note that in unions, the data members of a union ordinarily share a memory address.

This attribute is applied to a potentially empty data member so that the compiler can optimize it to occupy no memory. A data member with the [[no_unique_address]] attribute may share the address of another member. The syntax is as follows:

```
[[no_unique_address]] int x {};
```

Here is a complete example:

```
struct Empty {}; // empty strut
struct X {
    int i;
    Empty e;
};
struct Y {
    int i;
    [[no_unique_address]] Empty e;
};
int main() {
    // the size of any object of empty class type is at least 1
    static_assert(sizeof(Empty) >= 1);

    // at least one byte is needed to give e a unique address
    static_assert(sizeof(X) >= sizeof(int) + 1);

    // empty member optimized out
    static_assert(sizeof(Y) == sizeof(int));
    return 0;
}
```

Output: 0
# The expression

```
```text
b.none()
```
```

returns `true` if none of the bits is set in `bitset b` (that is, all the bits are `false`).

# The expressions

```
```text
b == b1
b != b1
```
```

compare the two `bitset`s for equality and inequality, respectively.

Each of the bitwise assignment operators `&=`, `|=` and `^=` (discussed in detail in **Section 22.5**) can be used to combine `bitset`s. For example,

```
```text
b &= b1;
```
```

performs a bit-by-bit logical AND between `bitset`s `b` and `b1`. The result is stored in `b`. Bitwise logical OR and bitwise logical XOR are
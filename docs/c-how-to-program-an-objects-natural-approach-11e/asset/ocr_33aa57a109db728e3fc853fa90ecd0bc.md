The expression

```
```text
b[bitNumber]
```
```

for a non-const bitset returns a `std::bitset::reference`^24 that enables you to manipulate the bool at position bitNumber; otherwise, it returns a copy of the bool.

The expression

```
```text
b.test(bitNumber);
```
```

performs range checking on bitNumber first. If bitNumber is in range (based on the number of bits in the bitset), test returns true if the bit is on or false if it’s off. Otherwise, test throws an out_of_range exception.

The expression

```
```text
b.size()
```
```

returns the number of bits.

The expression

```
```text
b.count()
```
```

returns the number of bits that are set (true).

The expression

```
```text
b.any()
```
```

returns true if any bit is set.

The expression

```
```text
b.all()
```
```

returns true if all of the bits are set (true).

The expression

```
```text
b.none()
```
```

returns true if none of the bits is set (that is, all the bits are false).

The expressions

```
```text
b == b1
b != b1
```
```

compare the two bitsets for equality and inequality, respectively.

Each of the bitwise assignment operators `&=`, `|=`, and `^=` can be used to combine bitsets. For example,

```
```text
b &= b1;
```
```

performs a bit-by-bit AND between b and b1, setting each bit in b “on” if it’s “on” in both b and b1. Bitwise OR

```
```text
b |= b1;
```
```

sets each bit in b “on” if it’s “on” in either or both of b and b1. Bitwise XOR

```
```text
b ^= b2;
```
```

sets each bit in b “on” if it’s “on” in only b and b1, but not both.

24. “std::bitset<N>::reference.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/utility/bitset/reference.
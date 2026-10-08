```
int main()
{
    constexpr int max = 10;
    for (bitset<max> b; cin >> b; ) {
        cout << b << "\n";
        for (int i = 0; i < max; ++i) cout << b[i]; // reverse order
        cout << "\n";
    }
}
```

If you need a more complete picture of **bitsets**, look them up in your online documentation, a manual, or an expert-level textbook.

# 25.5.3 Signed and unsigned

Like most languages, C++ supports both signed and unsigned integers. Unsigned integers are trivial to represent in memory: bit0 means 1, bit1 means 2, bit2 means 4, and so on. However, signed integers pose a problem: how do we distinguish between positive and negative numbers? C++ gives the hardware designers some freedom of choice, but almost all implementations use the two's complement representation. The leftmost (most significant bit) is taken as the “sign bit”:

![](bbox=[0.32, 0.51, 0.77, 0.59])

If the sign bit is 1, the number is negative. Almost universally, the two's complement representation is used. To save paper, we consider how we would represent signed numbers in a 4-bit integer:

| | | 1 | 2 | 4 | 7 |
|---|---|---|---|---|---|
| **Positive:** | 0 | 1 | 2 | 4 | 7 |
| | 0000 | 0001 | 0010 | 0100 | 0111 |
| **Negative:** | -1 | -2 | -3 | -5 | -8 |
| | 1111 | 1110 | 1101 | 1011 | 1000 |

The bit pattern for –(x+1) can be described as the complement of the bits in x (also known as ~x; see §25.5.1).
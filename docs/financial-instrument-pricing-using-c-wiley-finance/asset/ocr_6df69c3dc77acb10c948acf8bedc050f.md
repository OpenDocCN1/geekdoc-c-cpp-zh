The output in this case is `0011000`. We note that extra bits are *padded* from the left. The next example extracts 4 bits from the beginning of the input string:

```
int num_bits = 4;
index = 0;
bitset<7> bsE(string("10111000"), index, num_bits);
cout << "Bitset with start index and number bits: " << bsE << endl;
```

The output in this case is `0001011`. In both of the above cases we note that the bitset’s elements are constructed *from right to left.*

We now discuss the operations that modify the bits in a bitset in some way. For example, we can set all the bits to true, set all the bits to a given value, set all the bits to false, flip all the bits and flip at a certain position:

```
const int SZ = 4;
bitset<SZ> bsX(string("1010"));

bsX.set();                // Set all bits to true

// Set all the bits to bitValue.
bool bitValue = 1;   // True.
for (size_t j = 0; j < bsX.size(); ++j)
{
    bsX.set(j, bitValue);
}

bsX.reset();             // Set all bits to 0 (false).
bsX.flip();              // Set unset bits and vice versa.
bsX.flip(2);             // Toggle bit at position 2.
```

We have also created two utility functions to print the contents of a bitset and to compare two bitsets:

```
template <int N>
void ExamineBitset(const bitset<N>& bs)
{
    cout << "Number of total bits: " << bs.size() << endl;
    cout << "Number of set bits: " << bs.count() << endl;
    cout << "Is any bit set?: " << boolalpha << bs.any() << endl;
    cout << "Is no bit set?: " << boolalpha << bs.none() << endl;
}
```

```
template <int N>
void CompareBitsets(const bitset<N>& bs1, const bitset<N>& bs2)
{
    cout << "Bitsets equal?: " << boolalpha << (bs1 == bs2) << endl;
    cout << "BitSets not equal?: " << boolalpha << (bs1 != bs2) << endl;
}
```

You can test these functions and examine the output.
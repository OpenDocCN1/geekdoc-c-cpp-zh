# 10.3 C++ std::bitset<N> AND BOOST DYNAMIC BITSET LIBRARY

We discuss bitsets in this section. They model *fixed-size arrays* (in the case of STL) and *dynamic arrays* (in the case of Boost). Bitsets are useful when we wish to manage sets of flags and when we use bitwise operations (such as AND, OR) on these sets.

We first discuss the STL class `bitset<N>`. This class models fixed-size arrays of bits. The number of bits N is defined at compile-time and this value cannot be changed thereafter. The function categories in `bitset` are:

+   - Constructors: default constructors and constructors based on integer and string input arguments.
+   - Querying if one, some or all bits in a bitset have been set; comparing bitsets for equality or inequality.
+   - Setting, resetting and flipping the bits in a bitset.
+   - Bitwise operations on bitsets (and, or, nor, left and right shift, toggle bits).
+   - Type conversions: converting bitsets to `string` and to `long`.
+   - Counting the number of bits that have been set in a bitset.

We give some examples of how to use class `bitset`. We first create a default bitset, a bitset that we initialise using an integral value and then we create a bitset from a string:

```
#include <bitset>

// Constructors.
const int N = 10;
bitset<N> bsA;          // All bits set to 0.
cout << bsA << endl;   // Prints 10 zeroes.

int val = 7;
bitset<N> bsB(val);    // Init bitset with val's bit representation.
cout << bsB << endl;   // The binary form of val, i.e. 0000...111.

// Constructing bitsets based on strings.
bitset<N> bsC(string("0101010101"));   // String of length 10.
cout << bsC << endl;
```

Next, we create bitsets by extracting certain bits from input strings. In the first case we create a bitset of length 7 by extracting information starting at the third bit (index = 2) and continuing to the end of the string:

```
// Bitsets with start pos and/or size.
int index = 2;                         // 3rd bit, indexing
                                      // starts at 0.
bitset<7> bsD(string("1111000"), index);  // From index to end.
cout << "Bitset with start index: " << bsD << endl;
```
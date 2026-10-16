
```
array<int,7> a = {1,2,3,5,8,13,25};
auto x1 = get<5>(a); // 13
auto x2 = a[5]; // 13
auto sz = tuple_size<decltype(a)>::value; // 7
typename tuple_element<5,decltype(a)>::type x3 = 13; // x3 is an int
```

These type functions are for people writing code that expects tuples.
Use a constexpr function (§28.2.2) and a type alias (§28.2.1) to improve readability: auto sz = Tuple_size<decltype(a)>(); // 7
Tuple_element<5,decltype(a)> x3 = 13; // x3 is an int The tuple syntax is meant for use in generic code.

## 34.2.2 bitset

Aspects of a system, such as the state of an input stream (§38.4.5.1), are often represented as a set of flags indicating binary conditions such as good/bad, true/false, and on/off. C++ supports the notion of small sets of flags efficiently through bitwise operations on integers (§11.1.1). Class bitset<N> generalizes this notion and offers greater convenience by providing operations on a sequence of N bits [0:N), where N is known at compile time. For sets of bits that don’t fit into a long long int, using a bitset is much more convenient than using integers directly. For smaller sets, bitset is usually optimized. If you want to name the bits, rather than numbering them, the alternatives are to use a set (§31.4.3), an enumeration (§8.4), or a bit-field (§8.2.7).

A bitset<N> is an array of N bits. It is presented in <bitset>. A bitset differs from a vector<bool> (§34.2.3) by being of fixed size, from set (§31.4.3) by having its bits indexed by integers rather than associatively by value, and from both vector<bool> and set by providing operations to manipulate the bits.

It is not possible to address a single bit directly using a built-in pointer (§7.2). Consequently, bitset provides a reference-to-bit (proxy) type. This is actually a generally useful technique for addressing objects for which a built-in pointer for some reason is unsuitable:

```
template<size_t N>
class bitset {
public:

class reference { // reference to a single bit:
friend class bitset;
reference() noexcept;

public: // support zero-based subscripting in [0:b.size())
~reference() noexcept;
reference& operator=(bool x) noexcept; // for b[i] = x;
reference& operator=(const reference&) noexcept; // for b[i] = b[j];
bool operator~() const noexcept; // return ~b[i]
operator bool() const noexcept; // for x=b[i];
reference& flip() noexcept; // b[i].flip();
```
};
// ...

};

For historical reasons, **bitset** differs in style from other standard-library classes. For example, if an index (also known as a *bit position*) is out of range, an **out_of_range** exception is thrown. No iterators are provided. Bit positions are numbered from right to left in the same way bits often are in a word, so the value of **b[i]** is **pow(2,i)**. Thus, a bitset can be thought of as an **N**-bit binary number:

position: 9876543210 **bitset<10>(989)**: 1 1 1 1 0 1 1 1 0 1

### 34.2.2.1 Constructors

A **bitset** can be constructed with a specified number of zeros, from the bits in an **unsigned long long int**, or from a **string**:

### bitset<N> Constructors (§iso.20.5.1) (continues)

```
bitset bs {};
bitset bs {n};
bitset bs {s,i,n,z,o};
```

```
bitset bs {s,i,n,z}; bitset bs {s,i,n}; bitset bs {s,i}; bitset bs {s};
```

- **N** zero bits
- Bits from **n**; **n** is an **unsigned long long**
- **n** bits **[i:i+n]** of **s**; **s** is a **basic_string<C,Tr,A>**; **z** is the character of type **C** used for zero; **o** is the character of type **C** used for one; explicit

```
bitset bs {s,i,n,z,C{'1'}};
bitset bs {s,i,n,C{'0'},C{'1'}};
bitset bs {s,inpos,C{'0'},C{'1'}};
bitset bs {s,0,npos,C{'0'},C{'1'}};
```

### bitset<N> Constructors (continued) (§iso.20.5.1)

```
bitset bs {p,n,z,o};
bitset bs {p,n,z}; bitset bs {p,n}; bitset bs {p};
```

**n** bits **[p:p+n]**; **p** is a C-style string of type **C***; **z** is the character of type **C** used for zero; **o** is the character of type **C** used for one; explicit **bitset bs {p,n,z,C{'0'}}**;

```
bitset bs {p,n,C{'1'},C{'0'}};
bitset bs {p,npos,C{'1'},C{'0'}};
```

The position **npos** is **string<C>**’s “beyond the end” position, meaning “all characters until the end” (§36.3).

When an **unsigned long long int** argument is supplied, each bit in the integer is used to initialize the corresponding bit in the **bitset** (if any). A **basic_string** (§36.3) argument does the same, except that the character **‘0’** gives the bit value **0**, the character **‘1’** gives the bit value **1**, and other characters cause an **invalid_argument** exception to be thrown. For example:

```
void f()
{

bitset<10> b1; // all 0
bitset<16> b2 = 0xaaaa; // 1010101010101010
bitset<32> b3 = 0xaaaa; // 00000000000000001010101010101010
bitset<10> b4 {"1010101010"}; // 1010101010 bitset<10> b5 {"10110111011110",4}; // 0111011110

bitset<10> b6 {string{"1010101010"}}; // 1010101010
bitset<10> b7 {string{"10110111011110"},4}; // 0111011110 bitset<10> b8 {string{"10110111011110"},2,8}; // 0011011101

bitset<10> b9 {string{"n0g00d"}}; // invalid_argument thrown bitset<10> b10 = string{"101001"}; // error :no implicit string to bitset conversion
}
```

A key idea in the design of bitset is that an optimized implementation can be provided for bitsets that fit in a single word. The interface reflects this assumption.

### 34.2.2.2 bitset Operations

A bitset provides the operators for accessing individual bits and for manipulating all bits in the set: bitset<N> Operations (§iso.20.5) (continues)

- bs[i] The i th bit of bs
- bs.test(i) The i th bit of bs; throw out_of_range if i is not in [0:bs.size()) bs&=bs2 Bitwise and
- bs|=bs2 Bitwise or
- bs^=bs2 Bitwise exclusive or

### bitset<N> Operations (continued) (§iso.20.5)

- bs<< =n Logical left shift (fill with zeros)
- bs>> =n Logical right shift (fill with zeros)
- bs.set() Set every bit of bs to 1
- bs.set(i,v) bs[i]=v
- bs.reset() Set every bit of bs to 0
- bs.reset(i) b[i]=0;
- bs.flip() bs[i]=~bs[i] for every bit in bs
- bs.flip(i) bs[i]=~bs[i]
- bs2=~bs Make complement set: bs2=bs, bs2.flip()
- bs2=bs<<n Make left-shifted set: bs2=bs, bs2<< =n
- bs2=bs>>n Make right-shifted set: bs2=bs, bs2>> =n
- bs3=bs&bs2 Bitwise and: bs3[i]=bs[i]&bs2[i] for each bit in bs
- bs3=bs|bs2 Bitwise or: bs3[i]=bs[i]|bs2[i] for each bit in bs
- bs3=bs^bs2 Bitwise exclusive or: bs3[i]=bs[i]^bs2[i] for each bit in bs
- is>>bs Read from is into bs; is is an istream
- os<<bs Write bs to os; os is an ostream

The >> and << are I/O operators when their first operand is an iostream; othewise, they are shift operators and their second operand must be an integer. For example:

```
bitset<9> bs ("110001111"); cout << bs << '\n';
auto bs2 = bs<<3;
```

```
cout << bs2 << '\n';
cin >> bs;
bs2 = bs>>3;
cout << bs2 << '\n';
```

```
// write"110001111" to cout
// bs2 == "001111000";
// write"001111000" to cout
// read from cin
// bs2 == "000110001" if the input were "110001111" // write"000110001" to cout
```

When bits are shifted, a logical (rather than cyclic) shift is used. That implies that some bits “fall off the end” and that some positions get the default value 0. Note that because size_t is an unsigned type, it is not possible to shift by a negative number. It does, however, imply that b<<-1 shifts by a very large positive value, thus leaving every bit of the bitset b with the value 0. Your compiler should warn against this.

A bitset also supports common operations such as size(), ==, I/O, etc.:

### More bitset<N> Operations (§iso.20.5)

```
C, Tr, and A have defaults for basic_string<C,Tr,A>
n=bs.to_ulong() n is the unsigned long corresponding to bs
n=bs.to_ullong() n is the unsigned long long corresponding to bs
s=bs.to_string<C,Tr,A>(c0,c1) s[i]=(b[i])?c1:c0; s is a basic_string<C,Tr,A>
s=bs.to_string<C,Tr,A>(c0) s=bs.template to_string<C,Tr,A>(c0,C{'1'}) s=bs.to_string<C,Tr,A>() s=bs.template to_string<C,Tr,A>(C{'0'},C{'1'})
```

### Section 34.2.2.2 bitsetOperations 981

### More bitset<N> Operations (continued) (§iso.20.5)

```
C, Tr, and A have defaults for basic_string<C,Tr,A>
n=bs.count() n is the number of bits with value 1 in bs

n=bs.size() n is the number of bits in bs
bs==bs2 Do bs and b2 have the same value?
bs!=bs2 !(bs==bs2)
bs.all() Do all bits in bs have the value 1?
bs.any() Does any bit in bs have the value 1?
bs.none() Does no bit in bs have the value 1?
```

### hash<bitset<N>> Specialization of hash for bitset<N>

The operations to_ullong() and to_string() provide the inverse operations to the constructors. To avoid nonobvious conversions, named operations were preferred over conversion operators. If the value of the bitset has so many significant bits that it cannot be represented as an unsigned long, to_ulong() throws overflow_error; so does to_ullong() if its bitset argument doesn’t fit.

Fortunately, the template arguments for the basic_string returned by to_string are defaulted. For example, we could write out the binary representation of an int:

```
void binary(int i)
```

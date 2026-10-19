```
unsigned long to_ulong() const;
```

Returns: x.

Throws: overflow_error if the integral value x corresponding to the bits in *this cannot be represented as type unsigned long.

```
unsigned long long to_ullong() const;
```

Returns: x.

Throws: overflow_error if the integral value x corresponding to the bits in *this cannot be represented as type unsigned long long.

```
template<class charT = char,
    class traits = char_traits<charT>,
    class Allocator = allocator<charT>>
basic_string<charT, traits, Allocator>
to_string(charT zero = charT('0'), charT one = charT('1')) const;
```

Effects: Constructs a string object of the appropriate type and initializes it to a string of length N characters. Each character is determined by the value of its corresponding bit position in *this. Character position N - 1 corresponds to bit position zero. Subsequent decreasing character positions correspond to increasing bit positions. Bit value zero becomes the character zero, bit value one becomes the character one.

Returns: The created object.

```
size_t count() const noexcept;
```

Returns: A count of the number of bits set in *this.

```
constexpr size_t size() const noexcept;
```

Returns: N.

```
bool operator==(const bitset<N>& rhs) const noexcept;
```

Returns: true if the value of each bit in *this equals the value of the corresponding bit in rhs.

```
bool test(size_t pos) const;
```

Returns: true if the bit at position pos in *this has the value one.

Throws: out_of_range if pos does not correspond to a valid bit position.

```
bool all() const noexcept;
```

Returns: count() == size().

```
bool any() const noexcept;
```

Returns: count() != 0.

```
bool none() const noexcept;
```

Returns: count() == 0.

```
bitset<N> operator<<(size_t pos) const noexcept;
```

Returns: bitset<N>(*this) <<= pos.

```
bitset<N> operator>>(size_t pos) const noexcept;
```

Returns: bitset<N>(*this) >>= pos.

```
constexpr bool operator[](size_t pos) const;
```

Preconditions: pos is valid.

Returns: true if the bit at position pos in *this has the value one, otherwise false.

Throws: Nothing.
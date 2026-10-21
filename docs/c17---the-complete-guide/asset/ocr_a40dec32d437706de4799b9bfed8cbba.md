```
std::cout << std::numeric_limits<std::underlying_type_t<std::byte>>::digits;
```

Most of the time it is 8, but there are platforms where this is not the case.

# 18.2 std::byte Types and Operations

This section describes the types and operations of std::byte in detail.

# 18.2.1 std::byte Types

In the header file <cstddef>, the C++ standard library defines type std::byte as follows:

```
namespace std {
  enum class byte : unsigned char {
  };
}
```

That is, std::byte is nothing but a scoped enumeration type with some supplementary bit-wise operators defined:

```
namespace std {
  ...
  template<typename IntType>
    constexpr byte operator<< (byte b, IntType shift) noexcept;
  template<typename IntType>
    constexpr byte& operator<<= (byte& b, IntType shift) noexcept;
  template<typename IntType>
    constexpr byte operator>> (byte b, IntType shift) noexcept;
  template<typename IntType>
    constexpr byte& operator>>= (byte& b, IntType shift) noexcept;

  constexpr byte& operator|= (byte& l, byte r) noexcept;
  constexpr byte operator| (byte l, byte r) noexcept;
  constexpr byte& operator&= (byte& l, byte r) noexcept;
  constexpr byte operator& (byte l, byte r) noexcept;
  constexpr byte& operator^= (byte& l, byte r) noexcept;
  constexpr byte operator^ (byte l, byte r) noexcept;
  constexpr byte operator~ (byte b) noexcept;

  template<typename IntType>
    constexpr IntType to_integer (byte b) noexcept;
}
```
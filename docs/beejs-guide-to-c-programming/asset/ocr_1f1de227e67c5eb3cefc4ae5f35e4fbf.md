# Chapter 37

# Fixed Width Integer Types

C has all small, bigger, and biggest integer types like int and long and all that. And you can look in the section on limits to see what the largest int is with INT_MAX and so on.

How big are those types? That is, how many bytes do they take up? We could use sizeof to get that answer. But what if I wanted to go the other way? If I needed a type that was exactly 32 bits (4 bytes) or at 16 bits or somuch?

How can we declare a type that's a certain size?

The header <stdint.h> gives us a.

# 37.1 The Bit-Sized Types

For both signed and unsigned integers, we can specify a type that is a certain number of bits, with some caveats, of course.

And there are three main classes of these types (in these examples, the N would be replaced by a certain number of bits):

+   * Integers of exactly a certain size (int_N_t)
* Integers that are at least a certain size (int_least_N_t)
* Integers that are at least a certain size and are as fast as possible (int_fast_N_t)¹

How much faster is fast? Defined maybe amount faster. Probably. The spec doesn't say how much, just that 'they'll be the fastest on this architecture. Most C compilers are pretty good, so you'll probably only use this places in where the most possible speed needs to be guaranteed (rather than just hoping the compiler is producing pretty-dang-fast code, which it is).

Finally, unsigned numbers have a leading u to differentiate them.

For example, these types have the following listed meaning:

```
int32_t w;               // x is exactly 32 bits, signed
uint16_t x;              // y is exactly 16 bits, unsigned
int_least8_t y;          // y is at least 8 bits, signed
uint_fast64_t z;        // z is the fastest representation at least 64 bits, unsigned
```

> ¹Some architectures have different size data that the CPU and RAM operate with a faster rate than others. In those cases, if you need the fastest 8-bit number, it might give you a 16- or 32-bit type instead because that's faster. So with this, you won't know how big the type is, but it will be as fast as you bias
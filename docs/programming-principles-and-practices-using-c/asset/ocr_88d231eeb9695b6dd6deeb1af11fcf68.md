To quote John Bentley: "People who play with bits will be bitten" and "People who play with bytes will be bitten."

So, why do we manipulate bits? Sometimes the natural objects of our application simply are bits, so that some of the natural operations in our application domain are bit operations. Examples of such domains are hardware indicators ("flags"), low-level communications (where we have to extract values of various types out of byte streams), graphics (where we have to compose pictures out of several levels of images), and encryption (see the next section).

For example, consider how to extract (low-level) information from an integer (maybe because we wanted to transmit it as bytes, the way binary I/O does):

```
```c
void f(short val)              // assume 16-bit, 2-byte short integer
{
    unsigned char right = val&0xff;   // rightmost (least significant) byte
    unsigned char left = val>>8;      // leftmost (most significant) byte
    // ...
    bool negative = val&0x8000;      // sign bit
    // ...
}
```
```

Such operations are common. They are known as “shift and mask.” We “shift” (using `<<` or `>>`) to place the bits we want to consider to the rightmost (least significant) part of the word where they are easy to manipulate. We “mask” using `and (&)` together with a bit pattern (here `0xff`) to eliminate (set to zero) the bits we do not want in the result.

When we want to name bits, we often use enumerations. For example:

```
```cpp
enum Printer_flags {
    acknowledge=1,
    paper_empty=1<<1,
    busy=1<<2,
    out_of_black=1<<3,
    out_of_color=1<<4,
    // ...
};
```
```

This defines each enumerator to have exactly the value that its name indicates:

| Enumerator     | Decimal | Hex   | Binary     |
|:---------------|:--------|:------|:-----------|
| out_of_color   | 16      | 0x10  | 0001 0000  |
| out_of_black   | 8       | 0x8   | 0000 1000  |
| busy           | 4       | 0x4   | 0000 0100  |
| paper_empty    | 2       | 0x2   | 0000 0010  |
| acknowledge    | 1       | 0x1   | 0000 0001  |
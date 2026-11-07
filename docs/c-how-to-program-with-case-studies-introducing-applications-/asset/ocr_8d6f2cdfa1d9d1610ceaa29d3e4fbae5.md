# ### 10.10.3 Unnamed Bit Fields

An unnamed bit field is used as padding in a struct. For example, the definition

```
```
struct example {
    unsigned int a : 13;
    unsigned int   : 19;
    unsigned int b : 4;
};
```
```

uses an unnamed 19-bit field as padding. Nothing can be stored in those 19 bits. Mem-ber b (assuming a four-byte-word computer) is stored in a separate word of memory.

An unnamed bit field with a zero width aligns the next bit field on a new storage-unit boundary. For example, the struct

```
```
struct example {
    unsigned int a : 13;
    unsigned int   : 0;
    unsigned int   : 4;
};
```
```

uses an unnamed 0-bit field to skip the remaining bits (as many as there are) of the storage unit in which it is stored and to align b on the next storage-unit boundary.

# ### Self Check

+   1. *(Fill-In)* The structure definition

```
```
struct example {
    unsigned int a : 13;
    unsigned int   : 19;
    unsigned int b : 4;
};
```
```

uses an unnamed 19-bit field as ________—nothing can be stored in those 19 bits.
Answer: padding.

+   2. *(Multiple Choice)* Which of the following statements a), b) or c) about Section 10.10.1's `struct bitCard` is *false*?
+       a) A bit field is declared by following an `unsigned` or `signed` integral member name with a colon (:) and an integer constant representing the bit field's width.
+       b) The `struct bitCard` definition indicates that member `face` is stored in 4 bits, member `suit` is stored in 2 bits, and member `color` is stored in 1 bit.
+       c) The number of bits in a bit field is based on each structure member's desired range of values.
+       d) All of the above statements are true.

Answer: d.

# ### 10.11 Enumeration Constants

Section 5.11 introduced the keyword enum for defining a set of integer enumeration constants represented by identifiers. Values in an enum start with 0, unless specified otherwise, and increment by 1. For example, the enumeration
# 12.20 C Programming and Data Structures

Note that the field name follows a colon. The bit-length is decided by the range of value to be stored. The largest value that can be stored is 2^{n-1}, where n is bit-length. The internal representation of bit fields is machine dependent. That is, it depends on the size of int and the ordering of bits. Some machines store bits from left to right and others from right to left. The sketch below illustrates the layout of bit fields, assuming a 16-bit word that is ordered right to left.

![](bbox=[0.1, 0.3, 0.9, 0.42])

+   1. The first field always starts with the first bit of the word.
+   2. A bit field cannot overlap integer boundaries. That is, the sum of lengths of all the fields in a structure should not be more than the size of a word. In case, it is more, the overlapping field is automatically forced to the beginning of the next word.
+   3. There can be unnamed fields declared with size. Example:
+   
+   Unsigned : bit-length
+   
+   Such fields provide padding within the word.
+   4. There can be unused bits in a word.
+   5. We cannot take the address of a bit field variable. This means we cannot use scanf to read values into bit fields. We can neither use pointer to access the bit fields.
+   6. Bit fields cannot be arrayed.
+   7. Bit fields should be assigned values that are within the range of their size. If we try to assign larger values, behaviour would be unpredictable.

Suppose, we want to store and use personal information of employees in compressed form, this can be done as follows:

```
struct personal {
    unsigned sex : 1;
    unsigned age : 7;
    unsigned m_status : 1;
    unsigned children : 3;
    unsigned } emp;

```

This defines a variable name emp with four fields. The range of values each field could have is follows:

| Bit field | Bit length | Range of value |
|----------|------------|----------------|
| sex | 1 | 0 or 1 |
| age | 7 | 0 or 127 (2^7 - 1) |
| m_status | 1 | 0 or 1 |
| children | 3 | 0 to 7 (2^3 - 1) |
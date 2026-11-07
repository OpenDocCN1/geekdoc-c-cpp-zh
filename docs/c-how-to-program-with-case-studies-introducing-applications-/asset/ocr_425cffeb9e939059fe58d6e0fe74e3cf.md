**Answer:** A union shares its memory among all of its members. Only one member may be stored in a union at any time. You must keep track of which member is currently stored.

2. **(True/False)** The following union definition indicates that `number` is a union type with members `int x` and `double y`:

```
union number {
    int x;
    double y;
};
```

For a machine with four-byte ints and eight-byte doubles, the compiler must reserve at least 12 bytes for a variable of this union type. **Answer:** False. Only one of these members is active at a time, so the union needs to reserve only as much storage as is needed for the largest member—in this case, eight bytes.

# 10.9 **Bitwise Operators**

Computers represent all data internally as sequences of bits. Each bit can assume the value 0 or the value 1. On most systems, a sequence of eight bits forms a byte—the typical storage unit for a char variable. The bitwise operators are used to manipulate the bits of integral operands, both signed and unsigned, though unsigned integers are typically used. Bitwise data manipulations are machine-dependent. The following table summarizes the bitwise operators.

| Operator | Description |
|---|---|
| `&` — bitwise AND | Compares its two operands bit by bit. The bits in the result are set to 1 if the corresponding bits in the two operands are *both 1*. |
| `\|` — bitwise inclusive OR | Compares its two operands bit by bit. The bits in the result are set to 1 if *at least one* of the corresponding bits in the two operands is 1. |
| `^` — bitwise exclusive OR (also known as bitwise XOR) | Compares its two operands bit by bit. The bits in the result are set to 1 if the corresponding bits in the two operands are different. |
| `<<` — left shift | Shifts the bits of the first operand left by the number of bits specified by the second operand; fill from the right with 0 bits. |
| `>>` — right shift | Shifts the bits of the first operand right by the number of bits specified by the second operand; the method of filling from the left is machine-dependent when the left operand is negative. |
| `~` — complement | All 0 bits are set to 1, and all 1 bits are set to 0. This is often called toggling the bits. |
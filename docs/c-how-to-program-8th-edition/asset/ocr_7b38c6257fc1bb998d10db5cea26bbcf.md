cessing functions in `<cstring>`. In the next chapter, we continue our discussion of data structures by discussing *containers*—data structures defined in the C++ Standard Template Library. We also present the many algorithms defined in the STL as well.

# Summary

# Section 21.2 Structure Definitions

+   - Keyword `struct` (p. 793) begins every structure definition. Between the braces of the structure definition are the structure member declarations.
+   - A structure definition creates a new data type (p. 793) that can be used to declare variables.

# Section 21.3 typedef

+   - Creating a new type name with the `typedef` (p. 794) does not create a new type; it creates a name that’s synonymous with a type defined previously.

# Section 21.5 Bitwise Operators

+   - The bitwise AND operator (`&`; p. 797) takes two integral operands. A bit in the result is set to one if the corresponding bits in each of the operands are one.
+   - Masks (p. 799) are used with bitwise AND to hide some bits while preserving others.
+   - The bitwise inclusive OR operator (`|`; p. 797) takes two operands. A bit in the result is set to one if the corresponding bit in either operand is set to one.
+   - Each of the bitwise operators (except complement) has a corresponding assignment operator.
+   - The bitwise exclusive OR operator (`^`; p. 797) takes two operands. A bit in the result is set to one if exactly one of the corresponding bits in the two operands is set to one.
+   - The left-shift operator (`<<`) shifts the bits of its left operand left by the number of bits specified by its right operand. Bits vacated to the right are replaced with zeros.
+   - The right-shift operator (`>>`) shifts the bits of its left operand right by the number of bits specified in its right operand. Right shifting an unsigned integer causes bits vacated at the left to be replaced by zeros. Vacated bits in signed integers can be replaced with zeros or ones.
+   - The bitwise complement operator (`~`; p. 797) takes one operand and inverts its bits—this produces the one’s complement of the operand.

# Section 21.6 Bit Fields

+   - Bit fields (p. 806) reduce storage use by storing data in the minimum number of bits required. Bit-field members must be declared as `int` or `unsigned`.
+   - A bit field is declared by following an unsigned or `int` member name with a colon and the width of the bit field.
+   - The bit-field width must be an integer constant.
+   - If a bit field is specified without a name, the field is used as padding (p. 809) in the structure.
+   - An unnamed bit field (p. 809) with width 0 aligns the next bit field on a new machine-word boundary.

# Section 21.7 Character-Handling Library

+   - Function `islower` (p. 812) determines if its argument is a lowercase letter (a–z). Function `isupper` (p. 812) determines whether its argument is an uppercase letter (A–Z).
+   - Function `isdigit` (p. 811) determines if its argument is a digit (0–9).
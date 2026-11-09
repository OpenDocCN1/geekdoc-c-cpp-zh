**Table 1.2: Operators in C# 2010**

| Operator Category | Operator Symbol | Description |
|---|---|---|
| Shift | << (left shift operator) | Shifts the left-hand side operand towards left by the number of bits specified by the right-hand side operand, which has to be of int type. |
|  | >> (right shift operator) | Shifts the left-hand side operand towards right by the number of bits specified by the right-hand side operand, which has to be of int type. |
| Relational and type testing | < (less than operator) | Returns true if the left-hand side operand is less than the right-hand side operand. Otherwise, it returns false. |
|  | > (greater than operator) | Returns true if the left-hand side operand is greater than the right-hand side operand. Otherwise, it returns false. |
|  | <= (less than equal to operator) | Returns true if the left-hand side operand is less than or equal to the right-hand side operand. Otherwise, it returns false. |
|  | >= (greater than equal to operator) | Returns true if the left-hand side operand is greater than or equal to the right-hand side operand. Otherwise, it returns false. |
|  | is | Returns true if the left-hand side operand and the right-hand side operands are compatible. Otherwise, it returns false. |
|  | as | Performs conversion between reference types, if the types are compatible. Otherwise, it returns null. |
| Equality | == (equality operator) | Returns true if the value type operands have the same value, else returns false. For reference types (except string type), it returns true if the operands refer to the same object, else it returns false (value type and reference type are discussed later in this chapter). |
|  | != (inequality operator) | Returns true if both the operands are unequal, otherwise, it returns false. |
| Logical AND | & (logical AND) | Returns true if and only if all the operands are true. |
| Logical XOR | ^ (logical XOR) | Returns true if and only if only one of its operands is true. |
| Logical OR | \| (logical OR) | Returns true if and only if at least one of the operands is true. |
| Conditional AND | && (logical AND) | Performs logical AND on its Boolean operands. The right-hand side operand is evaluated only if the left-hand side operand evaluates to true. |
| Conditional OR | \|\| (logical OR) | Performs logical OR on its Boolean operands. The right-hand side operand is evaluated only if the left-hand side operand evaluates to false. |
| Null-coalescing | ?? (null-coalescing operator) | Returns one of the two values depending on the null values. It returns the left-hand side operand if its value is not null; otherwise, it returns the right-hand side operand. Only nullable data types support this operator. |
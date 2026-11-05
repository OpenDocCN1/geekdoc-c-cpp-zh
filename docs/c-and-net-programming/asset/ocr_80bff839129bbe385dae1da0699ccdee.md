# Output

Result of bln1&&bln2:bln3=False
Result of bln1 || bln2:bln3=True
Result of bln1:bln3=False

# 3.2.4 Bitwise Operators

# Concept

+   1. Bitwise operators perform operation on the binary representation of a numeric value.

# Explanation

+   2. Here is the list of Bitwise operators in the given table.

| Bitwise Operators | Description |
|---|---|
| & (Bitwise And operator) | This operator copies a bit to the result if it exists in both operands. |
| \| (Bitwise Or operator) | This operator copies a bit to the result if exists in either of the operand. |
| ~ (Bitwise Not operator) | This operator complement the value of the bit on which it is applied. |
| ^ (Bitwise Xor Operator) | This operator copies the bit if it is set in one operand but not both. |
| << (Bitwise Left Shift Operator) | The left operands value is moved left by the number of bits specified by the right operand. |
| >> (Bitwise Right Shift Operator) | The left operands value is moved right by the number of bits specified by the right operand. |

# Example

```
```csharp
// Illustration of bitwise operators.
using System;
namespace CSharpOperators
{
class Bitwise
{
static void Main()
{
int num1 = 10; // binary value of 10=1010
int num2 = 5; // binary value of 5=0101
int num3;
```
```
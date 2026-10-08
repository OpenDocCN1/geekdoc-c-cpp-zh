# Logical Operators

C# supports the below mentioned logical operators. In the table given below, assume variable A has a Boolean value true and B holds Boolean value as false.

| Operator | Description | Example |
|---|---|---|
|| | It is called logical OR operator. In case any of the two operands is nonzero then the condition becomes true. | (A || B) is true. |
| && | It is called Logical AND operator. In case both the operands are nonzero then condition becomes true | (A && B) is false. |
| ! | It is called Logical NOT operator. It is used to reverse the logical state of its operand. In case a condition is true then Logical NOT operator will make false. | !(A && B) is true. |

# Bitwise Operators

These operators work on bits and perform bit by bit operation. The truth tables for |, &, and ^ is as given below –

| p | q | p&q | p|q | p^q |
|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 | 0 |
| 1 | 1 | 1 | 1 | 0 |
| 1 | 0 | 0 | 1 | 1 |

Now let us assume that A = 60 and B = 13, then in the binary format –
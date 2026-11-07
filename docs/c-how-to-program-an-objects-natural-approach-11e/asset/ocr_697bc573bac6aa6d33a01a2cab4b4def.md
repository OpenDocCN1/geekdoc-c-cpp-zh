# 3.11 Compound Assignment Operators

You can abbreviate the statement

`c = c + 3;`

with the addition compound assignment operator, `+=`, as

`c += 3;`

The `+=` operator adds its right operand’s value to the left-side variable’s value, then stores the result in the left-side variable. Thus, the assignment expression `c += 3` adds 3 to `c`. The following table shows all the arithmetic compound assignment operators, sample expressions and explanations of what the operators do:

| Operator | Sample expression | Explanation | Assigns |
|---|---|---|---|
| *Assume: int c = 3, d = 5, e = 4, f = 6, g = 12:* | | | |
| `+=` | `c += 7` | `c = c + 7` | 10 to c |
| `-=` | `d -= 4` | `d = d - 4` | 1 to d |
| `*=` | `e *= 5` | `e = e * 5` | 20 to e |
| `/=` | `f /= 3` | `f = f / 3` | 2 to f |
| `%=` | `g %= 9` | `g = g % 9` | 3 to g |

# Checkpoint

+   1. *(Code)* Write a statement that uses a compound assignment operator to divide the variable `total` by 5.

Answer: `total /= 5;`

# 3.12 Increment and Decrement Operators

The following table summarizes C++’s two unary operators for adding 1 to or subtracting 1 from the value of a numeric variable—these are the unary increment operator, `++`, and the unary decrement operator, `--`:

| Operator | Operator name | Sample expression | Explanation |
|---|---|---|---|
| `++` | prefix increment | `++number` | Increment number by 1, then use the new value of number in the expression in which number resides. |
| `++` | postfix increment | `number++` | Use the current value of number in the expression in which number resides, then increment number by 1. |
| `--` | prefix decrement | `--number` | Decrement number by 1, then use the new value of number in the expression in which number resides. |
| `--` | postfix decrement | `number--` | Use the current value of number in the expression in which number resides, then decrement number by 1. |
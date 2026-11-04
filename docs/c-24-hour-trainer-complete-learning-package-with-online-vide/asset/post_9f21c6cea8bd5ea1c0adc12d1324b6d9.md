
For example, the following code gives you the same result as the previous code but without the pre-increment operator:

```
int x, y = 10;
y = y + 1;
x = 10 + y;
```

## Logical Operators

The logical operators perform calculations on boolean (true or false) values. They let you combine logical statements to form new ones.

Lesson 18 explains how to use these values to perform tests that let a program take action only under certain circumstances. For example, a program might pay an employee overtime if the employee is hourly and worked more than 40 hours in the last week.

Table 11-5 summarizes the boolean operators.

TABLE 11-5

| OPERATOR | MEANING |
|---|---|
| & | AND |
| \| | OR |
| ^ | XOR |
| ! | NOT |
| && | Conditional AND |
| \|\| | Conditional OR |

The & operator returns true if and only if both of its operands are true. For example, you must buy lunch if it's lunchtime and you forgot to bring a lunch today:

```
mustBuyLunch = isLunchTime & forgotToBringLunch;
```

The | operator returns true if either of its operands is true. For example, you can afford lunch if either you brought enough money or you have a credit card (or both):

```
canAffordLunch = haveEnoughMoney | haveCreditCard;
```

The ! operator returns true if its single operand is false. For example, if the cafeteria is not closed, you can have lunch there:

```
canHaveLunch = !cafeteriaIsClosed;
```

The conditional operators, which are also called short-circuit operators, work just like the regular ones except they don't evaluate their second operand unless they must. For example, consider the following AND statement:

```
mustBuyLunch = isLunchTime && forgotToBringLunch;
```

Suppose it's only 9:00 a.m. so isLunchTime is false. When the program sees this expression, it evaluates isLunchTime and then encounters the && operator. Because isLunchTime is false, the program already knows that mustBuyLunch must also be false no matter what value follows the && (in this case forgotToBringLunch). In that case, the program doesn't bother to evaluate forgotToBringLunch and that saves a tiny amount of time.

Similarly, consider the following OR statement:

```
canAffordLunch = haveEnoughMoney || haveCreditCard;
```

If you have enough money, haveEnoughMoney is true, so the program doesn't need to evaluate haveCreditCard to know that the result canAffordLunch is also true.

Because the conditional && and || operators are slightly faster, most developers use them whenever they can instead of using & and |.

> NOTE There is one case where the conditional operators may cause problems. If the second operand is not a simple value but the result returned from some sort of method call, then if you use a conditional operator, you cannot always know whether the method was called. This might matter if the method has side effects: consequences that last after the method has finished, like opening a database or creating a file. In that case, you cannot know later whether the database is open or the file is created. This is seldom a problem and you can avoid it completely by avoiding side effects.

## String Operators

The only string operator C# provides is +. This operator concatenates (joins) two strings together. For example, suppose the variable username contains the user's name. Then the following code concatenates the text "Hello " (note the trailing space) with the user's name and displays the result in a message box:

```
MessageBox.Show("Hello " + username);
```

Lesson 14 explains methods that you can use to manipulate strings: find substrings, replace text, check length, and so forth.

> **NOTE** One very non-obvious fact about string operations is that a string calculation does not really save the results in the same memory used by the variable on the left of an assignment statement. Instead it creates a new string holding the result of the calculation and makes the variable refer to that.
> 
> For example, consider the following code:
> 
> ```csharp
> string greeting = usernameTextBox.Text;
> greeting = "Hello " + greeting;
> ```
> 
> This looks like it saves a user's name in the variable greeting and then tacks "Hello" onto the front. Actually, the second statement creates a whole new string that holds "Hello" plus the user's name and then makes greeting refer to the new string.
> 
> For many practical applications, the difference is small, and you can ignore it. However, if you're performing a huge number of concatenations (perhaps in one of the loops described in Lesson 19), your program might have performance issues. The StringBuilder class can help address this issue, but it's a bit more advanced so I'm not going to cover it here. See msdn.microsoft.com/library/2839d5h5.aspx for more information.

## Comparison Operators

The comparison operators compare two values and return true or false depending on the values' relationship. For example, x < y returns true if x is less than y.

Table 11-6 summarizes the comparison operators.

### TABLE 11-6

| OPERATOR | MEANING | EXAMPLE |
|---|---|---|
| == | Equals | 2 == 3 is false |
| != | Not equals | 2 != 3 is true |
| < | Less than | 2 < 3 is true |
| <= | Less than or equal to | 2 <= 3 is true |
| > | Greater than | 2 > 3 is false |
| >= | Greater than or equal to | 2 >= 3 is false |

## Bitwise Operators

The bitwise operators enable you to manipulate the individual bits in integer values. For example, the bitwise | operator combines the bits in two values so the result has a bit equal to 1 wherever either of the two operands has a bit equal to one.

For example, suppose x and y are the byte values with bits 10000000 and 00000001. Then x | y has bits 10000001.

This may be easier to understand if you write y below x as in the following:

```
x:      10000000
 y:      00000001
         --------
 Result: 10000001
```

Now it's easy to see that the result has a 1 where either x or y had a 1.

The bitwise operators are fairly advanced so I'm not going to do much with them, but Table 11-7 summarizes them. The shift operators are not “bitwise” because they don't compare two operands one bit at a time, but they are bit-manipulation operators so they're included here.

### TABLE 11-7

| OPERATOR | MEANING | EXAMPLE |
|---|---|---|
| & | Bitwise AND | 11110000<br>& 00111100<br>= 00110000 |
| \| | Bitwise OR | 11110000<br>\| 00111100<br>= 11111100 |
| ^ | Bitwise XOR | 11110000<br>^ 00111100<br>= 11001100 |
| ~ | Bitwise complement | ~11110000<br>= 00001111 |
| << | Left shift | 11100111 << 2<br>= 10011100 |
| >> | Right shift (for signed types) | 11100111 >> 2<br>= 11111001 |
| >> | Right shift (for unsigned types) | 11100111 >> 2<br>= 00111001 |

If the operand has a signed type (such as sbyte, int, or long), then >> makes new bits on the left be copies of the value's sign bit (its leftmost bit). If the operand has an unsigned type (byte, uint, ulong), then >> makes the new bits 0.

All of these except ~ also have corresponding compound assignments operators, for example, &= and <<=. Compound assignment operators are described in the next section.

## Assignment Operators

The assignment operators set a variable (or property or whatever) equal to something else. The simplest of these is the = operator, which you have seen several times before. This operator simply assigns whatever value is on the right to the variable on the left.

The other assignment operators, which are known as compound assignment operators, combine the variable's current value with whatever is on the right in some way. For example, the following code adds 3 to whatever value x currently holds:

```
x += 3;
```

This has the same effect as the following statement that doesn't use the += operator:

```
x = x + 3;
```

Table 11-8 summarizes the assignment operators. For the examples, assume i is an int, x is a float, and a and b are bools.

### TABLE 11-8

| OPERATOR | MEANING | EXAMPLE | MEANS |
|---|---|---|---|
| = | Assign | x = 10; | x = 10; |
| += | Add and assign | x += 10; | x = x + 10; |
| -= | Subtract and assign | x -= 10; | x = x - 10; |
| *= | Multiply and assign | x *= 10; | x = x * 10; |
| /= | Divide and assign | x /= 10; | x = x / 10; |
| %= | Modulus and assign | x %= 10; | x = x % 10; |
| &= | Logical AND and assign | a &= b; | a = a & b; |
| \|= | Logical OR and assign | a \|= b; | a = a \| b; |
| ^= | Logical XOR and assign | a ^= b; | a = a ^ b; |
| <<= | Left shift and assign | i <<= 3; | i = i << 3; |
| >>= | Right shift and assign | i >>= 5; | i = i >> 5; |

## Precedence

Sometimes the order in which you evaluate the operators in an expression changes the result. For example, consider the expression 2 + 3 * 5. If you evaluate the + first, you get 5 * 5, which is 25, but if you evaluate the * first, you get 2 + 15, which is 17.

To prevent any ambiguity, C# defines operator precedence to determine which comes first.

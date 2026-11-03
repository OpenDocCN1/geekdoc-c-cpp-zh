
| Decimal | Abbreviation | Description |
|---:|---|---|
| 16 | DLE | Data link escape |
| 17 | DC1 | XON, with XOFF to pause listings |
| 18 | DC2 | Device control 2, block-mode flow control |
| 19 | DC3 | XOFF, with XON is TERM=18 flow control |
| 20 | DC4 | Device control 4 |
| 21 | NAK | Negative acknowledge |
| 22 | SYN | Synchronous idle |
| 23 | ETB | End transmission block, not the same as EOT |
| 24 | CAN | Cancel line, MPE echoes! |
| 25 | EM | End of medium, Control-Y interrupt |
| 26 | SUB | Substitute |
| 27 | ESC | Escape, next character is not echoed |
| 28 | FS | File separator |
| 29 | GS | Group separator |
| 30 | RS | Record separator, block-mode terminator |
| 31 | US | Unit separator |

The above is a list of all the control ASCII characters. Following is the list of printable ASCII characters in ASCII.

| Char | Dec | Description |
|---|---:|---|
| SP | 32 | Space |
| ! | 33 | Exclamation mark |
| " | 34 | Quotation mark |
| # | 35 | Cross hatch (number sign) |
| $ | 36 | Dollar sign |
| % | 37 | Percent sign |
| & | 38 | Ampersand |
| ' | 39 | Closing single quote (apostrophe) |
| ( | 40 | Opening parentheses |
| ) | 41 | Closing parentheses |
| * | 42 | Asterisk (star, multiply) |
| + | 43 | Plus |
| , | 44 | Comma |
| - | 45 | Hyphen, dash, minus |
| . | 46 | Period |
| / | 47 | Slant (forward slash, divide) |
| 0 | 48 | Zero |
| 1 | 49 | One |
| 2 | 50 | Two |
| 3 | 51 | Three |
| 4 | 52 | Four |
| 5 | 53 | Five |
| 6 | 54 | Six |
| 7 | 55 | Seven |
| 8 | 56 | Eight |
| 9 | 57 | Nine |
| : | 58 | Colon |
| ; | 59 | Semicolon |
| < | 60 | Less than sign |
| = | 61 | Equals sign |
| > | 62 | Greater than sign |
| ? | 63 | Question mark |
| @ | 64 | At-sign |
| A | 65 | Uppercase A |
| B | 66 | Uppercase B |
| C | 67 | Uppercase C |
| D | 68 | Uppercase D |
| E | 69 | Uppercase E |
| F | 70 | Uppercase F |
| G | 71 | Uppercase G |
| H | 72 | Uppercase H |
| I | 73 | Uppercase I |
| J | 74 | Uppercase J |
| K | 75 | Uppercase K |
| L | 76 | Uppercase L |
| M | 77 | Uppercase M |
| N | 78 | Uppercase N |
| O | 79 | Uppercase O |
| P | 80 | Uppercase P |
| Q | 81 | Uppercase Q |
| R | 82 | Uppercase R |
| S | 83 | Uppercase S |
| T | 84 | Uppercase T |
| U | 85 | Uppercase U |
| V | 86 | Uppercase V |
| W | 87 | Uppercase W |
| X | 88 | Uppercase X |
| Y | 89 | Uppercase Y |
| Z | 90 | Uppercase Z |
| [ | 91 | Opening square bracket |
| \\ | 92 | Reverse slant (Backslash) |
| ] | 93 | Closing square bracket |
| ^ | 94 | Caret (Circumflex) |
| _ | 95 | Underscore |
| \` | 96 | Opening single quote |
| a | 97 | Lowercase a |
| b | 98 | Lowercase b |
| c | 99 | Lowercase c |
| d | 100 | Lowercase d |
| e | 101 | Lowercase e |
| f | 102 | Lowercase f |
| g | 103 | Lowercase g |
| h | 104 | Lowercase h |
| i | 105 | Lowercase i |
| j | 106 | Lowercase j |
| k | 107 | Lowercase k |
| l | 108 | Lowercase l |
| m | 109 | Lowercase m |
| n | 110 | Lowercase n |
| o | 111 | Lowercase o |
| p | 112 | Lowercase p |
| q | 113 | Lowercase q |
| r | 114 | Lowercase r |
| s | 115 | Lowercase s |
| t | 116 | Lowercase t |
| u | 117 | Lowercase u |
| v | 118 | Lowercase v |
| w | 119 | Lowercase w |
| x | 120 | Lowercase x |
| y | 121 | Lowercase y |
| z | 122 | Lowercase z |
| { | 123 | Opening curly brace |
| \| | 124 | Vertical line |
| } | 125 | Closing curly brace |
| ~ | 126 | Tilde (approximate) |
| DEL | 127 | Delete (rubout), cross-hatch box |

## 2.6 Operators and Punctuators

Like every other programming language, C has many characters with certain meanings.

Examples include the Arithmetic operators which stand for the usual arithmetic operations of addition, subtraction, multiplication, division, and modulus, respectively.

Modulus in mathematics returns the remainder after dividing a number by another. For example, the value of "a modulus b" is obtained by taking the remainder after dividing a by b. % is the character used for Modulus operation in C. Thus, 15%7 has the answer 1, and 7 % 5 results in 2.

In a program, operators can be used to separate identifiers that are involved in an expression. Remember, an expression is a statement that ends with a semicolon. It is good practice to give whitespaces between each identifier and operators to give better readability but it is not necessary. Compiler ignores Whitespaces unless they are quoted in the code. So, the following statements are identical to the compiler,

```
X=A+B;

X = A + B ;
```

Context is very important in almost everything. Symbols change their meaning depending upon where and how they are used. For example consider the following two statements which use % symbol in two different contexts.

```
printf("Owner: %s\n", OWNER);

int x = 15 % 4 ;
```

The first % symbol is the start of a conversion specification, or format which is related to the identifier in the later part of the expression, whereas the second % symbol represents the modulus operator of mathematics.

Examples of punctuators include parentheses, braces, commas, and semicolons.

Consider the following code:

```
void main(void)
{
int a, b = 2, c = 3;
a = (b * (b + c));
}
```

The parenthesis used right after main are used as an operator. By rules, they are used to indicate that main is a function. After the parenthesis, the symbols “{”, “,”, “,”, “,”, “(”, “(”, “)”, “)” and “,” are all punctuators. Both operators and punctuators are collected by the compiler as tokens (characters), and along with white space, they serve to separate language elements like identifiers, constants, functions, keywords, operators and others.

Tokens depend on their context a lot. For example, as explained in the previous paragraph, the parentheses are sometimes used to indicate a function name while they can be used as punctuators as well. Another example is given by the expressions

```
C = a + b ;
++ a ;
a += b ;
```

They all use + as a character, but ++ and += are increment and assignment operators respectively while the first one is a simple arithmetic operator. This dependency of symbols meaning on context leads to the short but more effective programming language C.

C language has rules of precedence and associativity in operators. It is critical in nature as we do not want one statement to result in two different outputs. These rules do not fully determine evaluation because we give user the power to achieve the result of desire by mastering these rules. Since expressions inside parentheses are evaluated first, parentheses can be used to clarify or change the order operations are performed.

Consider the expression:

`Answer = 30 + ( 4 * 10 / 5 -20 ) ;`

The operator “(” has the highest precedence in this expression so we dissect it before anything else. Then we have three operators inside parentheses. Multiplication and division have equal precedence so we perform whatever comes first in the expression. In this case, we perform 4 * 10 and have a result of 40. We divide 40 by 5 and result is 8. We subtract 20 from 8 and the result is -12. Now that the parentheses are closed, we compute the operations outside them. We add -12 to 30 and the result is 18.

| Operator | Name | Description |
|---|---|---|
| / | Divide | Used for division of two numbers |
| % | Modulus | Used to find remainder after division of 2 numbers |
| ~ | Negation | Binary operator, used to invert the boolean value |
| & | Bitwise AND | Used to perform logical AND on every bit |
| \| | Bitwise OR | Used to perform logical OR on every bit |
| ^ | Power | Used to compute power of a number |
| << | Left Shift | Used to shift bits to the left |
| >> | Right Shift | Used to shift bits to the right |

Let us now see an example of using these operators in a program:

```
#include "iostream"

void main(void)
{

int A = 50, B = 17;

bool Alive =false;

printf("This is a Program to demonstrate use of Arithmetic Operators in C\n");

printf("Sum: %d\n", A + B);

printf("Difference: %d\n", A - B);

printf("Product: %d\n", A * B);

printf("Division: %d\n", A / B);

printf("Modulus: %d\n", A % B);

printf("Negation: %s\n", ~Alive? "true":"false");

printf("Bitwise AND: %d\n", A & B);

printf("Bitwise OR: %d\n", A | B);

printf("Bitwise XOR: %d\n", A^B);

printf("Left Shift: %d\n", A<<2);

printf("Right Shift: %d\n", A>>2);

system("pause");
}
```

![](img/6d3b01499498c82f19a5187d6ebfb7f1_70_0.png)

The first four operators are pretty common and straightforward so we'll not discuss them here. Modulus returns us the remainder after dividing one number by the other. A % B returns the remainder after dividing A by B. For instance, the example in our code divides 50 by 17, 2 is quotient while 16 is the remainder. The remainder is returned and printed. Remember, we can always assign this value by using assignment operators. Here, we just used the returned value to be printed once.

Negation operator is used to invert a binary number using 2's complement form. If the input is boolean, as is in our program, the result is inverted.

Then we have 5 Bitwise operators, starting with Bitwise AND operation. It performs logical AND on each bit of the numbers provided. For example, in our program, we have

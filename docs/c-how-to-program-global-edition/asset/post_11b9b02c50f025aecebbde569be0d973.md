
Figure 10.15 shows the precedence and associativity of the various operators introduced to this point in the text. They're shown top to bottom in decreasing order of precedence.

| Operator | Associativity | Type |
|---|---|---|
| () [] . -> ++ (postfix) -- (postfix) | left to right | highest |
| + - ++ -- ! & * ~ sizeof (type) | right to left | unary |
| * / % | left to right | multiplicative |
| + - | left to right | additive |
| << >> | left to right | shifting |
| < <= > >= | left to right | relational |
| == != | left to right | equality |
| & | left to right | bitwise AND |
| ^ | left to right | bitwise XOR |
| | | left to right | bitwise OR |
| && | left to right | logical AND |
| || | left to right | logical OR |
| ?: | right to left | conditional |
| = += -= *= /= &= |= ^= <<= >>= %= | right to left | assignment |
| , | left to right | comma |

Fig. 10.15 | Operator precedence and associativity.

## 10.10 Bit Fields

C enables you to specify the number of bits in which an unsigned or signed integral member of a structure or union is stored. This is referred to as a bit field. Bit fields enable better memory utilization by storing data in the minimum number of bits required. Bit field members must be declared as int or unsigned int.

### 10.10.1 Defining Bit Fields

Consider the following structure definition:

```
struct bitCard {
    unsigned int face : 4;
    unsigned int suit : 2;
    unsigned int color : 1;
};
```

which contains three unsigned int bit fields—face, suit and color—used to represent a card from a deck of 52 cards. A bit field is declared by following an unsigned or signed integral member name with a colon (:) and an integer constant representing the width of the field (i.e., the number of bits in which the member is stored). The constant representing the width must be an integer between 0 (discussed in Section 10.10.3) and the total number of bits used to store an int on your system, inclusive. Our examples were tested on a computer with 4-byte (32-bit) integers.

```c
wDeck[i].suit = i / (CARDS / 4);
wDeck[i].color = i / (CARDS / 2);
}

// output cards in two-column format; cards 0-25 indexed with
// k1 (column 1); cards 26-51 indexed with k2 (column 2)
void deal(const Card * const wDeck)
{
printf("%-6s%-6s%-15s%-6s%-6s\n", "Card", "Suit", "Color",
"Card", "Suit", "Color");

// loop through wDeck
for (size_t k1 = 0, k2 = k1 + 26; k1 < CARDS / 2; ++k1, ++k2) {
printf("Card:%3d Suit:%2d Color:%2d ", wDeck[k1].face, wDeck[k1].suit, wDeck[k1].color);
printf("Card:%3d Suit:%2d Color:%2d\n", wDeck[k2].face, wDeck[k2].suit, wDeck[k2].color);
}
}
```

Fig. 10.16 | Representing cards with bit fields in a struct. (Part 2 of 2.)

Card values 0-12 correspond to Ace through King
Suit values 0-3 correspond Hearts, Diamonds, Clubs and Spades
Color values 0-1 correspond to red and black

| Card | Suit | Color | Card | Suit | Color |
|------|------|-------|------|------|-------|
| 0 | 0 | 0 | 0 | 2 | 1 |
| 1 | 0 | 0 | 1 | 2 | 1 |
| 2 | 0 | 0 | 2 | 2 | 1 |
| 3 | 0 | 0 | 3 | 2 | 1 |
| 4 | 0 | 0 | 4 | 2 | 1 |
| 5 | 0 | 0 | 5 | 2 | 1 |
| 6 | 0 | 0 | 6 | 2 | 1 |
| 7 | 0 | 0 | 7 | 2 | 1 |
| 8 | 0 | 0 | 8 | 2 | 1 |
| 9 | 0 | 0 | 9 | 2 | 1 |
| 10 | 0 | 0 | 10 | 2 | 1 |
| 11 | 0 | 0 | 11 | 2 | 1 |
| 12 | 0 | 0 | 12 | 2 | 1 |
| 0 | 1 | 0 | 0 | 3 | 1 |
| 1 | 1 | 0 | 1 | 3 | 1 |
| 2 | 1 | 0 | 2 | 3 | 1 |
| 3 | 1 | 0 | 3 | 3 | 1 |
| 4 | 1 | 0 | 4 | 3 | 1 |
| 5 | 1 | 0 | 5 | 3 | 1 |
| 6 | 1 | 0 | 6 | 3 | 1 |
| 7 | 1 | 0 | 7 | 3 | 1 |
| 8 | 1 | 0 | 8 | 3 | 1 |
| 9 | 1 | 0 | 9 | 3 | 1 |
| 10 | 1 | 0 | 10 | 3 | 1 |
| 11 | 1 | 0 | 11 | 3 | 1 |
| 12 | 1 | 0 | 12 | 3 | 1 |

Fig. 10.17 | Output of the program in Fig. 10.16.

## Performance Tip 10.2

Bit fields help reduce the amount of memory a program needs.

## Portability Tip 10.9

Bit-field manipulations are machine dependent.

## Common Programming Error 10.12

Attempting to access individual bits of a bit field as if they were elements of an array is a syntax error. Bit fields are not "arrays of bits."

## Common Programming Error 10.13

Attempting to take the address of a bit field (the & operator may not be used with bit fields because they do not have addresses).

## Performance Tip 10.3

Although bit fields save space, using them can cause the compiler to generate slower-executing machine-language code. This occurs because it takes extra machine-language operations to access only portions of an addressable storage unit. This is one of many examples of the kinds of space-time trade-off that occur in computer science.

### 10.10.3 Unnamed Bit Fields

It's possible to specify an unnamed bit field to be used as padding in the structure. For example, the structure definition

```
struct example {
    unsigned int a : 13;
    unsigned int  : 19;
    unsigned int b : 4;
};
```

uses an unnamed 19-bit field as padding—nothing can be stored in those 19 bits. Member b (on our 4-byte-word computer) is stored in another storage unit. An unnamed bit field with a zero width is used to align the next bit field on a new storage-unit boundary. For example, the structure definition

```
struct example {
    unsigned int a : 13;
    unsigned int  : 0;
    unsigned int b : 4;
};
```

uses an unnamed 0-bit field to skip the remaining bits (as many as there are) of the storage unit in which a is stored and to align b on the next storage-unit boundary.

## 10.11 Enumeration Constants

An enumeration (discussed briefly in Section 5.11), introduced by the keyword enum, is a set of integer enumeration constants represented by identifiers. Values in an enum start with 0, unless specified otherwise, and are incremented by 1. For example, the enumeration

```c
enum months {
  JAN, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC
};
```

creates a new type, enum months, in which the identifiers are set to the integers 0 to 11, respectively. To number the months 1 to 12, use:

```c
enum months {
  JAN = 1, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC
};
```

Because the first value in the preceding enumeration is explicitly set to 1, the remaining values are incremented from 1, resulting in the values 1 through 12. The identifiers in any enumeration accessible in the same scope must be unique. The value of each enumeration constant of an enumeration can be set explicitly in the definition by assigning a value to the identifier. Multiple members of an enumeration can have the same constant value. In the program of Fig. 10.18, the enumeration variable month is used in a for statement to print the months of the year from the array monthName. We've made monthName[0] the empty string "". You could set monthName[0] to a value such as ***ERROR*** to indicate that a logic error occurred.

> **Common Programming Error 10.14**
> Assigning a value to an enumeration constant after it's been defined is a syntax error.

> **Good Programming Practice 10.5**
> Use only uppercase letters in enumeration constant names. This makes these constants stand out in a program and reminds you that enumeration constants are not variables.

```c
1 // Fig. 10.18: fig10_18.c
2 // Using an enumeration
3 #include <stdio.h>
4
5 // enumeration constants represent months of the year
6 enum months {
7   JAN = 1, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC
8 };
9
10 int main(void)
11 {
12    // initialize array of pointers
13    const char *monthName[] = { "", "January", "February", "March",
14    "April", "May", "June", "July", "August", "September", "October",
15    "November", "December" };
16
17    // loop through months
18    for (enum months month = JAN; month <= DEC; ++month) {
19        printf("%2d%s\n", month, monthName[month]);
20    }
21 }
```

```
1  January
2  February
3  March
4  April
5  May
6  June
7  July
8  August
9  September
10 October
11 November
12 December
```

Fig. 10.18 | Using an enumeration. (Part 2 of 2.)

## 10.12 Anonymous Structures and Unions

Earlier in this chapter we introduced structs and unions. C11 now supports anonymous structs and unions that can be nested in named structs and unions. The members in a nested anonymous struct or union are considered to be members of the enclosing struct or union and can be accessed directly through an object of the enclosing type. For example, consider the following struct declaration:

```
struct MyStruct {
    int member1;
    int member2;

    struct {
        int nestedMember1;
        int nestedMember2;
    }; // end nested struct
}; // end outer struct
```

For a variable myStruct of type struct MyStruct, you can access the members as:

```
myStruct.member1;
myStruct.member2;
myStruct.nestedMember1;
myStruct.nestedMember2;
```

## 10.13 Secure C Programming

Various CERT guidelines and rules apply to this chapter's topics. For more information on each, visit www.securecoding.cert.org.

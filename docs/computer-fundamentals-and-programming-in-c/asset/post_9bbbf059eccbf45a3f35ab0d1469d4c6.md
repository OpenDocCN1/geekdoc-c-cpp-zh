
## Advanced C

### Learning Objectives

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_462_0.png)

After studying this chapter, the readers will be able to

- explain bitwise operators and their uses
- discuss how command-line arguments can be passed and used
- discuss the C preprocessor, its directives, and predefined identifiers
- list the three data type qualifiers—const, volatile, and restrict
- use the data type qualifier restrict with pointers, functions, blocks, and structures
- comprehend variable-length argument list and its uses
- discuss different memory models and their application

### 16.1 INTRODUCTION

This chapter deals with some of the topics that typically fall in the domain of advanced use of C. The features discussed in this chapter may not be required for general applications, but may be essential and extremely advantageous for certain specific cases.

Preprocessing is the first step in the C program compilation stage, which is an important feature of the C compiler. In C, all preprocessor directives begin with a #. It is used to define constants or any macro substitution.

It has been discussed in an earlier chapter that pointers provide control over low-level memory operations. There are many programs that operate at a low level when individual bytes are operated on. The combination of pointers and bit-level operators makes C useful for many low-level applications and can almost replace assembly code. UNIX is mostly written in C.

Type qualifiers include the keywords const and volatile. The const qualifier places the assigned variable in the constant data area of memory which makes the particular variable unmodifiable. volatile is used less frequently and it indicates that the value can be modified outside the control of the program.

A function usually takes a number of arguments whose types are fixed when its code is compiled. But sometimes it is desirable to implement a function where the number of arguments is not constant or not known beforehand, when the function is written. For example, the printf function is a special type of routine that takes a variable number of arguments. The user-defined function may use variable-length argument list. The declaration requires a special syntax to indicate the fact that beyond a certain argument, the number and type of the parameters cannot be checked at compile time. Instead, the number and type of the parameters has to be computed at run time. Using ellipsis in the signature denotes a variable argument list.

### 16.2 BITWISE OPERATOR

Since a computer understands only machine language, data is represented as binary numbers that are various combinations of 0's and 1's. Readers are conversant with the binary number system and the binary arithmetic. Table 16.1 lists the bitwise operators that may be used to manipulate binary numbers.

Bitwise operators allow the user to read and manipulate bits in variables of certain types. It is to be remembered that bitwise operators only work on two types—int and char. Bitwise operators fall into two categories—binary bitwise operators and unary bitwise operators. Binary operators take two arguments while unary operators take only one. The ~ (bitwise NOT) is a unary bitwise operator as it acts on a single operand. The &, |, ^, and ~ are known as bitwise logical operators. The >> and << are termed as bitwise shift operators. Bitwise operators, like arithmetic operators, do not change the value of the operands. Instead, a temporary value is created. This can then be assigned to a variable.

**Table 16.1 Bitwise operators used in C**

| Operator | Description |
| --- | --- |
| & | Bitwise AND |
| \| | Bitwise OR |
| ^ | Bitwise Exclusive OR |
| ~ | Bitwise Complement |
| << | Bitwise Shift Left |
| >> | Bitwise Shift Right |

Arithmetic operators are used in conjunction with the assignment operator to form shorthand forms that do the desired operation as well as assignment. Such forms are +=, -=, *=, and so on. These shorthand forms can also be applied to bitwise operators. For example, |=, &=, and ^= are some of the shorthand forms with bitwise operators. Nearly all binary operators have a version with = after it. These operators do change the value of the operands.

Arithmetic operators have higher precedence than bitwise operators. The precedence and associativity of bitwise operators are given in Table 16.2.

**Table 16.2 Precedence and associativity of bitwise operators and logical operators**

| Operator | Associativity |
| --- | --- |
| << >> | L→R |
| < <= > >= | L→R |
| == != | L→R |
| & | L→R |
| ^ | L→R |
| \| | L→R |
| && | L→R |
| \|\| | L→R |
| ?: | R→L |
| = += -= <<= >>= &= ^= \|= | R→L |

It is evident from the table that among bitwise operators, bitwise shift operators (<< and >>) have higher precedence than bitwise logical operators and bitwise compound operators (>>=, <<=, &=, ^=, and |=).

### Uses of bitwise operations

- Bitwise operators can be used to set or clear any bit in an integer.
- They can be used to quickly multiply and divide integers.
- They are most often used in coding device and low-level applications as they can be used to mask off certain bits.

Assuming that unsigned ints use 32 bits of memory, two variables X and Y are defined for illustration as

```
X = x31x30 ... x0
Y = y31y30 ... y0
```

Each bit of X and Y is referred to by writing the variable name in lowercase with the appropriate subscript numbers.

### 16.2.1 Bitwise AND

The bitwise AND is true only if both the corresponding bits in the operands are set. The following chart defines the operation of ‘&’ operator by applying ANDing on individual bits.

| x_i | y_i | x_i & y_i |
| --- | --- | --- |
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_463_0.png)

However, here is an example of bitwise ‘&’ operation applied on numbers represented by four bits.

| Variable | Decimal equivalent | b3 | b2 | b1 | b0 |
| --- | --- | --- | --- | --- | --- |
| x | 12 | 1 | 1 | 0 | 0 |
| y | 10 | 1 | 0 | 1 | 0 |
| z = x & y | 8 | 1 | 0 | 0 | 0 |

The & operator can be used to check whether a number is a power of 2 or not. This can be achieved by using the while loop and the arithmetic operator % as follows.

### EXAMPLE 1

```
#include <stdio.h>
int main()
{
    int n, r;
    printf("\n ENTER THE NUMBER :");
    scanf("%d", &n);
    while(n>1)
    {
        r=n%2;
        if(r==0)
            n=n/2;
        else
            break;
    }
    if(n!=1)
        printf("\n The number is not power of 2 ");
    else
        printf("\n The number is power of 2 ");
    return 0;
}
```

r is assigned the value obtained as remainder from this expression.

Using bitwise AND, the program in Example 1 can be rewritten without using the loop or the arithmetic operators.

```
#include <stdio.h>
int main()
{
    int n;
    printf("\n ENTER THE NUMBER :");
    scanf("%d", &n);
    if((n & (n-1))==0)
        printf("\n The number is power of 2 ");
    else
        printf("\n The number is not power of 2 ");
    return 0;
}
```

Bitwise operation

For illustration, let n = 8, n & (n − 1) evaluates to 0000. Here n is represented as four binary digits. Hence

| n & (n − 1) | 1 | 0 | 0 | 0 |
| --- | --- | --- | --- | --- |
| n | 1 | 0 | 0 | 0 |
| n − 1 | 0 | 1 | 1 | 1 |
| n & (n − 1) | 0 | 0 | 0 | 0 |

So, the number 8 is a power of 2. But, when n = 12, then

|  | 1 | 1 | 0 | 0 |
| --- | --- | --- | --- | --- |
| n | 1 | 1 | 0 | 0 |
| n − 1 | 1 | 0 | 1 | 1 |
| n & (n − 1) | 1 | 0 | 0 | 0 |

Thus, n & (n−1) is not equal to 0. Therefore, it is not a power of 2, though n is divisible by 2.

Masking is a process by which a given bit pattern is converted into another bit pattern by means of a logical bitwise operator. One of the operands in the bitwise operation is the original bit pattern that is to be transformed. The other operand, called mask, is the selected bit pattern that yields the desired conversion. The bitwise AND operator, &, is often used to mask off some set of bits. The following segment of code uses a mask with the value 1 and prints an alternating sequence of 0’s and 1’s.

```
int i, mask=1;
for(i=0; i<16; ++i)
    printf("%d", i & mask);
```

A mask value can be used to check if certain bits have been set. For example, to check whether bits 1 and 3 were set, the number should be masked with 10 and the result tested against the mask.

### EXAMPLE 2

```
#include <stdio.h>
int main()
{
    int n, mask = 10;
    printf("Enter a number: ");
    scanf("%d", &n);
    if((n & mask) == mask)
        printf("Bits 1 and 3 are set");
    else
        printf("Bits 1 and 3 are not set");
    return 0;
}
```

The above example is better understood with the following illustration:

| Variable | Contents | Remarks |
| --- | --- | --- |
| n | any decimal number; binary (16 bits) | x = 0 or 1; byte (most significant); byte (least significant) |
| mask | 10; 0000 0000 0000 1010 |  |
| n & mask | 0000 0000 0000 0000 / 0000 0000 0000 1010 / 0000 0000 0000 1000 | byte (most significant); byte (least significant); Bit number |

In case the value of n & mask is equal to mask, that is, if the bits 1 and 3 marked as x are equal to 1, then the bits in 1 and 3 positions are set to 1. Another important example of mask is 255; its binary equivalent is 0000 0000 1111 1111. As only the lower order


```
// accounted for
seconds = seconds % 60;
// Report the results
std::cout << hours << ":";
// Compute tens digit of minutes
int tens = minutes / 10;
std::cout << tens;
// Compute ones digit of minutes
int ones = minutes % 10;
std::cout << ones << ":";
// Compute tens digit of seconds
tens = seconds / 10;
std::cout << tens;
// Compute ones digit of seconds
ones = seconds % 10;
std::cout << ones << "\n";
}
```

Listing 4.12 (enhancedtimeconv.cpp) uses the fact that if x is a one- or two-digit number, x / 10 is the tens digit of x. If x / 10 is zero, x is necessarily a one-digit number.

## 4.8 Integers vs. Floating-point Numbers

Floating-point numbers offer some distinct advantages over integers. Floating-point numbers, especially doubles, have a much greater range of values than any integer type. Floating-point numbers can have fractional parts and integers cannot. Integers, however, offer one big advantage that floating-point numbers cannot—exactness. To see why integers are exact and floating-point numbers are not, we will explore the way computers store and manipulate the integer and floating-point types.

Computers store all data internally in binary form. The binary (base 2) number system is much simpler than the familiar decimal (base 10) number system because it uses only two digits: 0 and 1. The decimal system uses 10 digits: 0, 1, 2, 3, 4, 5, 6, 7, 8, and 9. Despite the lack of digits, every decimal integer has an equivalent binary representation. Binary numbers use a place value system not unlike the decimal system. Figure 4.4 shows how the familiar base 10 place value system works.

Figure 4.4 The base 10 place value system

| ... | 10⁵ | 10⁴ | 10³ | 10² | 10¹ | 10⁰ |
| --- | --- | --- | --- | --- | --- | --- |
| ... | 4 | 7 | 3 | 4 | 0 | 6 |
| ... | 100,000 | 10,000 | 1,000 | 100 | 10 | 1 |

473,406 = 4 x 10⁵ + 7 x 10⁴ + 3 x 10³ + 4 x 10² + 0 x 10¹ + 6 x 10⁰
= 400,000 + 70,000 + 3,000 + 400 + 0 + 6
= 473,406

With 10 digits to work with, the decimal number system distinguishes place values with powers of 10. Compare the base 10 system to the base 2 place value system shown in Figure 4.5.

Figure 4.5 The base 2 place value system

| ... | 2⁵ | 2⁴ | 2³ | 2² | 2¹ | 2⁰ |
| --- | --- | --- | --- | --- | --- | --- |
| ... | 1 | 0 | 0 | 1 | 1 | 1 |
| ... | 32 | 16 | 8 | 4 | 2 | 1 |

100111₂ = 1 × 2⁵ + 0 × 2⁴ + 0 × 2³ + 1 × 2² + 1 × 2¹ + 1 × 2⁰
= 32 + 0 + 0 + 4 + 2 + 1
= 39

With only two digits to work with, the binary number system distinguishes place values by powers of two. Since both binary and decimal numbers share the digits 0 and 1, we will use the subscript 2 to indicate a binary number; therefore, 100 represents the decimal value _one hundred_, while 100₂ is the binary number _four_. Sometimes to be very clear we will attach a subscript of 10 to a decimal number, as in 100₁₀.

In the decimal system, it is easy to add 3 + 5:

```
  3
+ 5
---
  8
```

The sum 3 + 9 is a little more complicated, as early elementary students soon discover:

```
  3
+ 9
---
```

The answer, of course, is 12, but there is no single _digit_ that means 12—it takes two digits, 1 and 2. The sum is

```
  1
  03
+ 09
---
  12
```

We can say 3 + 9 is 2, _carry the 1_. The rules for adding binary numbers are shorter and simpler than decimal numbers:

```
0₂ + 0₂ = 0₂
0₂ + 1₂ = 1₂
1₂ + 0₂ = 1₂
1₂ + 1₂ = 10₂
```

We can say the sum 1₂ + 1₂ is 0₂, _carry the_ 1₂. A typical larger sum would be

```
   11
9₁₀ = 1001₂
+ 3₁₀ = 0011₂
-------
12₁₀ = 1100₂
```

### 4.8.1 Integer Implementation

Mathematical integers are whole numbers (no fractional parts), both positive and negative. Standard C++ supports multiple integer types: `int`, `short`, `long`, and `long long`, `unsigned`, `unsigned short`, `unsigned long`, and `unsigned long long`. These are distinguished by the number of bits required to store the type, and, consequently, the range of values they can represent. Mathematical integers are infinite, but all of C++’s integer types correspond to finite subsets of the mathematical integers. The most commonly used integer type in C++ is int. All ints, regardless of their values, occupy the same amount of memory, and therefore use the same number of bits. The exact number of bits in an int is processor specific. A 32-bit processor, for example, is built to manipulate 32-bit integers very efficiently. A C++ compiler for such a system most likely would use 32-bit ints, while a compiler for a 64-bit machine might represent ints with 64 bits. On a 32-bit computer, the numbers 4 and 1,320,002,912 both occupy 32 bits of memory.

For simplicity, we will focus on unsigned integers, particularly the unsigned type. The unsigned type in Visual C++ occupies 32 bits. With 32 bits we can represent 4,294,967,296 different values, and so Visual C++’s unsigned type represents the integers 0 ... 4,294,967,295. The hardware in many computer systems in the 1990s provided only 16-bit integer types, so it was common then for C++ compilers to support 16-bit unsigned values with a range 0 ... 65,535. To simplify our exploration into the properties of computer-based integers, we will consider an even smaller, mythical unsigned integer type that we will call unsigned tiny. C++ has no such unsigned tiny type as it has a very small range of values—too small to be useful as an actual type in real programs. Our unsigned tiny type uses only five bits of storage, and Table 4.3 shows all the values that a variable of type unsigned tiny can assume.

Table 4.3: The unsigned tiny values

| Bits: Bit String | Decimal Value |
| :--- | :--- |
| 00000 | 0 |
| 00001 | 1 |
| 00010 | 2 |
| 00011 | 3 |
| 00100 | 4 |
| 00101 | 5 |
| 00110 | 6 |
| 00111 | 7 |
| 01000 | 8 |
| 01001 | 9 |
| 01010 | 10 |
| 01011 | 11 |
| 01100 | 12 |
| 01101 | 13 |
| 01110 | 14 |
| 01111 | 15 |
| 10000 | 16 |
| 10001 | 17 |
| 10010 | 18 |
| 10011 | 19 |
| 10100 | 20 |
| 10101 | 21 |
| 10110 | 22 |
| 10111 | 23 |
| 11000 | 24 |
| 11001 | 25 |
| 11010 | 26 |
| 11011 | 27 |
| 11100 | 28 |
| 11101 | 29 |
| 11110 | 30 |
| 11111 | 31 |

Table 4.3 shows that the unsigned tiny type uses all the combinations of 0s and 1s in five bits. We can derive the decimal number 6 directly from its bit pattern:

```
00110 => 0 0 1 1 0 => 0 x 16 + 0 x 8 + 1 x 4 + 1 x 2 + 0 x 1 = 6
```

To see that arithmetic works, try adding 4 + 3:

```
4₁₀ = 00100₂
+ 3₁₀ = 00011₂
-------
7₁₀ = 00111₂
```

That was easy since it involved no carries. Next we will try 3 + 1:

```
3₁₀ = 00011₂
+ 1₁₀ = 00001₂
-------
4₁₀ = 00100₂
```

In the ones column (rightmost column), 1₂ + 1₂ = 10₂, so write a 0 and carry the 1 to the top of the next column to the left (that is, the twos column). In the twos column, 1₂ + 1₂ + 0₂ = 10₂, so we must carry a 1 into the fours column as well.

The next example illustrates a limitation of our finite representation. Consider the sum 8 + 28:

```
   11
8₁₀ = 01000₂
+ 28₁₀ = 11100₂
-------
36₁₀ = 100100₂
```

In this sum we have a carry of 1 from the eights column to the 16s column, and we have a carry from the 16s column to nowhere. We need a sixth column (a 32s column), another place value, but our **unsigned tiny** type is limited to five bits. That carry out from the 16s place is lost. The largest **unsigned tiny** value is 31, but 28 + 8 = 36. It is not possible to store the value 36 in an **unsigned tiny** just as it is impossible to store the value 5,000,000,000 in a C++ unsigned int variable.

Consider exceeding the capacity of the **unsigned tiny** type by just one:

```
   11111
31₁₀ = 11111₂
+ 1₁₀ = 00001₂
-------
0₁₀ = 100000₂
```

Adding one to the largest possible **unsigned tiny**, 31, results in the smallest possible value, 0! This mirrors the behavior of the actual C++ **unsigned** type, as Listing 4.13 (unsignedoverflow.cpp) demonstrates.

### Listing 4.13: unsignedoverflow.cpp

```
#include <iostream>

int main() {
    unsigned x = 4294967293; // Almost the largest possible unsigned value
    std::cout << x << " + 1 = " << x + 1 << " \n";
    std::cout << x << " + 2 = " << x + 2 << " \n";
    std::cout << x << " + 3 = " << x + 3 << " \n";
}
```

Listing 4.13 (unsignedoverflow.cpp) prints

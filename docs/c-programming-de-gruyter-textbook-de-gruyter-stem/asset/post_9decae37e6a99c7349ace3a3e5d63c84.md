
## 1.4 Representation and Storage of Information

Computers can process data information, although it is conducted by control information. So the information in computers can be classified into two categories:

- information
- control information
- control word
- numerical information
- fixed point
- floating point
- data information
- character data
- nonnumeric information
- logical data

This chapter focuses on data information. Please refer to related books on hardware for details on control information.

### 1.4.1 Digital System of Computers

People are familiar with the decimal numerical system. However, almost all computers use the binary system. Computers cannot transfer, store, or process data until it is coded into binary digits. In programming, we usually transfer binary system into the octal system or hexadecimal system. A common feature to all these numerical systems is that they are positional numerical systems.

Generally speaking, if there are R basic symbols in a numerical system, we call it an R-based numerical system. R is the "base" of the numerical system and each position in the numerical system has a value called "weight".

The coding of positional numerical system complies with the "standing-on-R" rule, which means weight is the power based on R. Any number can be expanded to a polynomial according to the weight. For example, a decimal number 256.47 can be expanded into the polynomial as follows:

```
256.47 = 2 \times 10^2 + 5 \times 10^1 + 6 \times 10^0 - 4 \times 10^{-1} + 7 \times 10^{-2}
```

For any R-based number x, its value V(x) can be presented as:

```
V(x) = \sum_{i=0}^{n-1} x_i R^i + \sum_{i=-1}^{m} x_i R^i
```

Here m and n are integers, and R^l is the weight in Position i. X_0 and X_{-1} are separated by a decimal point. Usually, X_i should satisfy the following condition:

```
0 \leq X_i < R
```

## 10 Introduction

Tab. 1.1: Some numerical systems.

| Radix | Base | Carry Principle | Basic symbols |
| --- | --- | --- | --- |
| Binary | 2 | every 2 carries 1 | 0,1 |
| Octal | 8 | every 8 carries 1 | 0,1,2,3,4,5,6,7 |
| Decimal | 10 | every 10 carries 1 | 0,1,2,3,4,5,6,7,8,9,A,B,C,D,E |
| Hexadecimal | 16 | every 16 carries 1 | 0,1,2,3,4,5,6,7,8,9,A,B,C,D,E,F |

Note: A–F in the hexadecimal numerical system correspond to 10–15 in the decimal system.

In other words, R-based numerical systems use 0 ~ (R –1) numerical notations.
Table 1.1 presents some common systems.
In the binary system, the base is 2 and the weight of each position is a power of 2, following the principle of “every 2 into 1”. There are two basic symbols: 0 and 1. Here is an example of a number in the binary system:

1011.01

Nearly all computers use the binary numerical system for coding because of its following advantages:

### 1. Convenient for Physical Implementation

There are many physical devices with two different stable states, such as on and off states of gate circuit, high level, and low level of voltage. These states exactly correspond to the two symbols of 0 and 1. However, if the decimal numerical system is adopted, it would be really difficult if we tried to make a physical circuit with ten stable states.

### 2. Easy Mathematical Operations

It is proven that there are R(R +1) arithmetic rules for summation and quadrature in an R-based numerical system. If we use the decimal numerical system, we will have 55 different arithmetic rules while there are only three different rules if we use the binary numerical system, which further simplifies the designs of physical devices such as Arithmetic Logic Unit (ALU).

### 3. High Reliability

Since the voltage level (high or low) and current existence (with or without) are all related to two states, the binary system has strong anti-interference capability and high reliability for information.

### 4. Versatility

The binary system suits not only numerical information but also logical information encoding. Particularly, since only the two symbols of 0 and 1 correspond to two states, it is very convenient for computers to implement logic.

## 1.4 Representation and Storage of Information

Although computers use binary numerical system to encode information, the communication between computers and the outside world is still through hardware and software. It is self-evident that there are some disadvantages in binary system compared to other systems.

### 1.4.2 Conversions among Numeral Systems

#### R-based to Decimal

We get the decimal value of an R-based number by multiplying each digit by its weight and summing the results. For example:

```
1011.01 = 1 \times 2^3 + 0 \times 2^2 + 1 \times 2^1 + 1 \times 2^0 + 0 \times 2^{-1} + 1 \times 2^{-2}
```

#### Decimal to R-based

To convert a decimal number into an R-based system, we divide the number by R repeatedly and get the remainders. The remainders constitute the digits of the R-based number. For example, we can convert the decimal value 68 into binary number:

```
68 / 2 = 34, remainder 0
34 / 2 = 17, remainder 0
17 / 2 = 8, remainder 1
8 / 2 = 4, remainder 0
4 / 2 = 2, remainder 0
2 / 2 = 1, remainder 0
1 / 2 = 0, remainder 1
so 68_{10} = 1000100_2
```

To convert $68_{10}$ into an octal number, we can divide it by 8 and get the remainders:

```
68 / 8 = 8, remainder 4
8 / 8 = 1, remainder 0
1 / 8 = 0, remainder 1
so 68_{10} = 104_8
```

To convert $68_{10}$ into hexadecimal number, we can divide it by 16 and get the remainders:

```
68 / 16 = 4, remainder 4
4 / 16 = 0, remainder 4
so 68_{10} = 44_{16}
```

#### Decimal fraction to R-based fraction

When a decimal fraction is converted into an R-based number, we can multiply the decimal fraction by R continuously, and the integer array we get constructs the R-based fraction. This method is named “multiply by R and get the integers”:
can convert a decimal fraction to the R-based fraction like:

```
$V = \frac{X_{-1}}{R^1} + \frac{X_{-2}}{R^2} + \frac{X_{-3}}{R^3} + \dots + \frac{X_{-m}}{R^m}$
```

Multiplying both sides of the equation by $R$, we get:

```
$V \times R = X_{-1} + (\frac{X_{-2}}{R^1} + \frac{X_{-3}}{R^2} + \dots + \frac{X_{-m}}{R^{m-1}}) = X_{-1} + F_1$
```

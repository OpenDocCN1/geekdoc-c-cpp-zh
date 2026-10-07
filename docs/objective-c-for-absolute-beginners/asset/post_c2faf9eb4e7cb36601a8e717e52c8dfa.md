
over 200 million transistors, up from 149 million transistors on the A4 processor that was in iPhone 4 and the first iPad. See Figure 3–1.

![](img/322e107ddf8f5cd963a6efafdcd86f38_48_0.png)

# Moore's Law

The number of transistors on your iPhone or iPad’s processor is directly related to your device's processing speed, memory capacity, and the sensors (accelerometer, gyroscope) available in the device. The more transistors, the more powerful your device is.

In 1965, the cofounder of Intel, Gordon E. Moore, described the trend of transistors in a processor. He observed that the number of transistors in a processor doubled every 18 months from 1958 to 1965 and would likely continue “for at least 18 months.” The observation became famously known as “Moore’s Law” and have proven accurate for more than 55 years. See Figure 3–2.

# CPU Transistor Counts 1971-2008 & Moore's Law

![](img/322e107ddf8f5cd963a6efafdcd86f38_49_0.png)

Figure 3–2. Moore's Law

NOTE: There is a downside to Moore's Law and you have probably felt it in your pocket book. The problem with rapidly increasing processing capability is that it renders technology obsolete quickly. When your iPhone's two-year cell phone contract is up, the new iPhones on the market will be twice as powerful as the iPhone you had when you signed up. How convenient for everyone!

# Bytes

A byte is another unit used to describe information storage on computers. A byte is composed of 8 bits and a convenient power of 2. Whereas a bit can represent to two different values, a byte can represent up to 2^8 or 256 different values. A byte can contain values from 0–255.

NOTE: In Chapter 13, we discuss Base-2, Base-10, and Base-16 number systems in more detail. However, it is necessary to have an introduction to these systems in this chapter to understand data types.

The binary number system represents numerical symbols 0 and 1. To illustrate how the number 71 would be represented in binary, we will use a simple table of 8 bits (1 byte), with each bit represented as a power of 2. To convert the byte value 01000111 to decimal, simply add the bits. See Table 3–1.

# Table 3-1. The number 71 represented as a byte

| Power to 2 | $2^7$ | $2^6$ | $2^5$ | $2^4$ | $2^3$ | $2^2$ | $2^1$ | $2^0$ |
|---|---|---|---|---|---|---|---|---|
| Value "on" bit | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| Actual bit | 0 | 0 | 0 | 1 | 0 | 1 | 1 | 1 |

To represent the number 22 in binary, turn on the bits that add up to 22 or 00100110. See Table 3–2.

# Table 3-2. The number 22 represented as a byte

| Power to 2 | $2^7$ | $2^6$ | $2^5$ | $2^4$ | $2^3$ | $2^2$ | $2^1$ | $2^0$ |
|---|---|---|---|---|---|---|---|---|
| Value "on" bit | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| Actual bit | 0 | 0 | 1 | 0 | 0 | 1 | 1 | 0 |

To represent the number 255 in binary, turn on the bits that add up to 255 or 11111111. See Table 3–3.

# Table 3-3. The number 255 represented as a byte

| Power to 2 | $2^7$ | $2^6$ | $2^5$ | $2^4$ | $2^3$ | $2^2$ | $2^1$ | $2^0$ |
|---|---|---|---|---|---|---|---|---|
| Value "on" bit | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| Actual bit | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |

To represent the number 0 in binary, turn on the bits that add up to 0 or 00000000. See Table 3–4.

# Table 3-4. The number 0 represented as a byte

| Power to 2 | $2^7$ | $2^6$ | $2^5$ | $2^4$ | $2^3$ | $2^2$ | $2^1$ | $2^0$ |
|---|---|---|---|---|---|---|---|---|
| Value "on" bit | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| Actual bit | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

# Hexadecimal

Often, we use hexadecimal characters in another format that is recognized by computers, namely hexadecimal format. When you are debugging your code, the Hexadecimal system is a base-16 number system. It uses 16 distinct symbols, 0-9 to represent values zero to nine, and A, B, C, D, E, and F to represent values ten to fifteen. For example, the hexadecimal number 2AF3 is equal in decimal to (2 × 16³) + (10 × 16²) + (15 × 16), or 9995. Figure 3-3 shows the ASCII table of characters. One byte can represent 256 characters, which works well for Western characters. For example, hexadecimal 20 represents a space.

Hexadecimal 2D represents a "."

| Dec | Oct | Hex | Bin | Dec | Oct | Hex | Bin | Dec | Oct | Hex | Bin | Dec | Oct | Hex | Bin |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 000 | 0 | 0000000 | 32 | 040 | 20 | 0100000 | 64 | 100 | 40 | 0100000 | 96 | 140 | 60 | 1100000 |
| 1 | 001 | 1 | 0000001 | 33 | 041 | 21 | 0100001 | 65 | 101 | 41 | 0100001 | 97 | 141 | 61 | 1100001 |
| 2 | 010 | 2 | 0000010 | 34 | 042 | 22 | 0100010 | 66 | 102 | 42 | 0100010 | 98 | 142 | 62 | 1100010 |
| 3 | 011 | 3 | 0000011 | 35 | 043 | 23 | 0100011 | 67 | 103 | 43 | 0100011 | 99 | 143 | 63 | 1100011 |
| 4 | 100 | 4 | 0000100 | 36 | 044 | 24 | 0100100 | 68 | 104 | 44 | 0100100 | 100 | 144 | 64 | 1000000 |
| 5 | 101 | 5 | 0000101 | 37 | 045 | 25 | 0100101 | 69 | 105 | 45 | 0100101 | 101 | 145 | 65 | 1000001 |
| 6 | 110 | 6 | 0000110 | 38 | 046 | 26 | 0100110 | 70 | 106 | 46 | 0101110 | 102 | 146 | 66 | 1000010 |
| 7 | 111 | 7 | 0000111 | 39 | 047 | 27 | 0100111 | 71 | 107 | 47 | 0101111 | 103 | 147 | 67 | 1000011 |
| 8 | 100 | 8 | 0001000 | 40 | 050 | 28 | 0101100 | 72 | 110 | 48 | 0111000 | 104 | 148 | 68 | 1001100 |
| 9 | 101 | 9 | 0001001 | 41 | 051 | 29 | 0101101 | 73 | 111 | 49 | 0111001 | 105 | 149 | 69 | 1001101 |
| 10 | 110 | A | 0001010 | 42 | 052 | 30 | 0111110 | 74 | 112 | 50 | 0111010 | 106 | 150 | 70 | 1001110 |
| 11 | 111 | B | 0001011 | 43 | 053 | 31 | 0111111 | 75 | 113 | 51 | 0111111 | 107 | 151 | 71 | 1001111 |
| 12 | 110 | C | 0001100 | 44 | 054 | 32 | 1111110 | 76 | 114 | 52 | 1111110 | 108 | 152 | 72 | 1111111 |
| 13 | 111 | D | 0001111 | 45 | 055 | 33 | 1111111 | 77 | 115 | 53 | 1111111 | 109 | 153 | 73 | 1111111 |
| 14 | 110 | E | 0001110 | 46 | 056 | 34 | 1111110 | 78 | 116 | 54 | 1111100 | 110 | 154 | 74 | 1111111 |
| 15 | 111 | F | 0001111 | 47 | 057 | 35 | 1111111 | 79 | 117 | 55 | 1111111 | 111 | 155 | 75 | 1111111 |

![](img/322e107ddf8f5cd963a6efafdcd86f38_51_0.png)

Source: www.LookupTables.com

Figure 3–3. ASCII characters

# Unicode

Representing characters by a byte worked well for computers until about the 1990s, when the personal computer became widely adopted in non-Western countries where languages have more than 256 characters. Instead of a 1-byte character set, Unicode can have up to a 4-byte character set.

In order to facilitate faster adoption, the first 256 code points are indicial to the ASCII character table. Unicode can have different character encodings. The most common encoding used for Western text is called UTF-8. As an iPhone developer, you will probably use this character encoding the most.

# Data Types

Now that we've discussed how computers manipulate data, we need to cover a very concept called data types. Humans generally just look at data and the context in which it is used to determine what type of data it is and how it will be used. Computers need to be told how to do this. The programmer needs to tell the computer the type of data it is given. For example,

2 + 2 = 4.

The computer needs to know to add two numbers together. In this example, they are integers. You might first believe that adding these numbers is obvious to even the most casual observer, let alone a sophisticated computer. However, it is common for users of iPhone apps to store data as a series of characters, not a calculation. For example, a text message might read

> "Everyone knows that 2 + 2 = 4"

In this case, we are using our previous example in a series of characters called a string. A data type is simply the declaration to our program that defines the data we want to store. A variable is stored to store data and is declared with an associated data type. All data is stored in a variable and the variable has to have a variable type. For example, in Objective-C, the following are variable declarations with their data types.

```
int x = 10;
int y = 2;
int z = 0;
char prefix = 'c';
NSString *submarineName = "@USS Nevada SSBN-733";
```

Data types cannot be mixed with one another. You cannot do the following,

z = x + submarineName;

Mixing data types will cause either compiler warnings or compiler errors and your app will not run.

Most data you will use in your programs can be classified into three different types—Boolean, numbers, and objects. We will discuss how to work with numbers and object

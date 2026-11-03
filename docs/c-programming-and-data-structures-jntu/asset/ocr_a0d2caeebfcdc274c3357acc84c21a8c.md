The primary data types and their extensions are discussed in this section. The user-defined data types are defined in the next section while the derived data types such as arrays, functions, structures and pointers are discussed as and when they are encountered. The empty data set is discussed in the chapter on functions.

All C compilers support four fundamental data types, namely integer (int), character (char), floating point (float), and double-precision floating point (double). Many of them also offer extended data types such as long int and long double. Various data types and the terminology used to describe them are given in Fig. 3.4. The range of the basic four types are given in Table 3.5. We discuss briefly each one of them in this section.

![](bbox=[0.18, 0.38, 0.85, 0.68])

Fig. 3.4 Primary data types in C

# Table 3.5 Size and Range of Basic Data Types

| Data type | Range of values |
|---|---|
| char | −128 to 127 |
| int | −32,768 to 32,767 |
| float | 3.4e−38 to 3.4e+38 |
| double | 1.7e−308 to 1.7e+308 |

# Integer Types

Integers are whole numbers with a range of values supported by a particular machine. Generally, integers occupy one word of storage, and since the word sizes of machines vary (typically, 16 or 32 bits) the size of an integer that can be stored depends on the computer. If we use a 16 bit word length, the size of the integer value is limited to the range −32768 to +32767 (that is, −2^15 to 2^15−1). A signed integer
bits the mantissa. In computers that have fixed word length, the proportion of bits for exponents and bits for the mantissa should be appropriate. However, if we want to satisfy requirements both in range and precision, we usually use a double word or even more words to store a floating-point number.

# 1.4.7 Representation of Non-numerical Information

In computers, non-numerical information is also encoded 0 and 1. Here we will focus on the coding schemes for Chinese and Western characters.

The most popular coding scheme for western characters is “American Standard Code for Information Interchange”, shortened as ASCII code. It includes 10 numbers, 95 printable characters including upper and lower English characters and 33 control characters. ASCII code uses 7 bits of a byte to represent a character and can represent most 2¹¹⁸ characters.

Since ASCII code does not use the most significant bit in a byte, many systems use this as the check bit to improve the transmission reliability.

Aside from ASCII, there is another code called EBCDIC (Extended Binary Decimal Interchange code), which uses 8 bits to represent a character. EBCDIC can then represent most 256 characters.

So how can we represent Chinese characters in computers? There are many Chinese characters (at least thousands of ordinary characters) compared to English characters, and obviously one by (of eight digits) is far from enough. Now we have two-byte, three-byte or even four-byte code schemes for Chinese characters and the most popular is “Chinese Standard Code for Information Interchange”(GB2312-80), shortened as GB code. GB code is a two-byte code scheme, and it uses seven bits of each byte to encode a Chinese character.

Chinese coding and Western coding coexists in a computer. How to distinguish them is important, because different types of information have different process modes. One method is to set the most significant bits in each pair of bytes in GB2312-80 as “1”, while keeping the most significant bit in each byte in ASCII code as “0”. Then software (or hardware) can distinguish them.

# 1.5 The Development Process of Programs

Before we start learning programming, let's get a basic understanding of the development process of a program and learn some elementary terms. In the following chapters, readers may gain a deeper comprehension of the knowledge.
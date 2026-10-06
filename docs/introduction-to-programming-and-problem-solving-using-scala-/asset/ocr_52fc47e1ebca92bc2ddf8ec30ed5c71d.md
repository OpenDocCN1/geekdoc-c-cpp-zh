The last one is interesting. When you check if it makes sense, remember that negative values are represented using two's complement and an Int has 32 bits.

There are two other bitwise operators that are worth mentioning. They are left-shift and right-shift and are written in Scala as << and >>. These operators shift the bits in an integer value if you think about the meaning of bits, like multiplying or dividing by powers of two in the same way that adding zeros to the end of a decimal number is the same as multiplying by powers of two. Some simple examples show how you can use this to get powers of.

```
scala= 1 << 0
res7: Int = 1
```

```
scala= 1 << 1
res8: Int = 2
```

```
scala= 1 << 2
res9: Int = 4
```

```
scala= 1 << 3
res10: Int = 8
```

Let's look at some of these closer. The decimal 1 is represented as 00000001 in binary and << shifting zero bits to the left, thus the result unchanged and decimal 1. However, 1 << 1 shifts 1 bit to the left. Shifting 1 bit to left changes 00000001 to 00000010 which is decimal 2. If we start with the decimal 1 and perform 1 << 2, this shifts 2 bits to the left. Shifting 2 bits to left changes 00000001 to 00000100 which is decimal 4. There is a second version of right-shift using >>>. The normal version does not move the sign bit so signs are preserved. The second version will not this and shift the sign bit down with everything else.

You might wonder why you would want to do these things. Using a single integer value as a collection of Boolean values is common in libraries based on the C language and frequently appears in operating system code. There is another usage that could interest you projects later in life. If you have adjusted settings on a computer you have probably seen that colors can be represented as 8-bit, 16-bit, 24-bit, or 32-bit values. Given the abundance of memory on modern computers, the most of time will use 32-bit color. Have you ever written a web page or looked at a web page with colors represented as hexadecimal digits.

The first two specify how much red, the next two specify how much green, and the last two specify how much blue. This is RGB for reasons and it is exactly 24-bit color. 32-bit color uses an alpha channel because computers can operate more quickly with memory in 32-bit chunks because they are typically dealt with a 32-bit integer. The additional bits stores the alpha channel which is for transparency. It does not matter much for your screen, but it is something that can be used to nice effect in 2-graphics which we will discuss in chapter 12.

32-bit color is often called ARGB because it has alpha, red, green and blue values packed into 32 bits. Each has 8 bits or a byte. This is where bitwise operations come into play. You might be given four different values for alpha, red, green, and blue for a color and need to pack them together into a single 32-bit integer. Alternately, you might be given a single ARGB value as a 32-bit integer and have to figure out the individual components. Indeed, both of these appear as exercises below.
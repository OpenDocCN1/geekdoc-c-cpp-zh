# Dive 1

# All You Need Are Bits

> "*Bits are the raw material out of which we fashion the world.*"

If there is a single characteristic that sets C programmers apart, it is an understanding of bits. If you don’t understand bits then you are a programmer in some other language pretending to be a C programmer. Harsh, but true. Most accounts of bit patterns start off from binary values then move on to two’s complement and finally, sometimes floating-point, but this simply hides the fact that bits aren’t any of these things. Let’s start at the beginning.

# States

A bit is a two-state system – a bit can be a 1 or a 0. It doesn’t matter what you call these two states, true and false will do, but so will up and down or on and off and many more. Computers work in terms of groups of bits which can be accessed and worked with as a single unit. Typically the size of the group is eight bits, that is a byte. While this isn’t strictly necessary, we’ll use it in our examples which would be similar for a different number of bits.

The eight bits in a byte are usually have a particular order and are generally numbered starting from the right:

```
```
7 6 5 4 3 2 1 0
x x x x x x x x
```
```

Bit 0 is generally called the “lowest” or “least significant bit” and bit 7 is called the “highest” or “most significant bit”. The reason for this terminology comes from regarding the group of bits as a binary number. Notice that we need to make an “endian” decision. Which end to number bits from is arbitrary and depends on the machine’s architecture, but this big-endian numbering is almost universal. The reason for this will become apparent when we deal with place value systems later.
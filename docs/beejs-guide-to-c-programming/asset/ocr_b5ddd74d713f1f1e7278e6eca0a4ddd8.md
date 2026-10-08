# Chapter 23. Pointers III: Pointers to Pointers and More

What we have here is a struct foo's built in such a way that encourage a compiler to inject padding bytes (though it doesn't have). And then we get an unsigned char * to the first byte of the struct foo variable x.

From here all we need to know the sizeof x and we can loop through many bytes, printing out the values (in hex for ease).

Running this gives a bunch of numbers as output. I have annotated it below to identify where the values were stored:

```
| x.a == 0x12

AB |
BF | padding bytes with "random"
26 |

78 |
56 | x.b == 0x12345678
34 |
12 |
```

On all systems, sizeof(char) is 1, and we see first byte at the top of the output holding the value 0x12 that we stored.

Then we have padding bytes—for me, we can see those 4 bytes at the end. Notice how they're the same bytes as are in the hex value 0x12345678, but strangely in reverse order.

So that's a little peek under the hood of a more complex entity in memory.

# 23.3 The NULL Pointer and Zero

These things can be used interchangeably:

+   * NULL
* '\0'
* (void)*

Personally I always use NULL when I mean NULL, but you might see some other variants from time to time. Though '\0' (with all bits set to zero) will also compare equal, it's *weird* to compare it to a pointer; you should compare NULL the pointer. (Of course, lots times in string processing, you're comparing the pointer pointers to '\0', and that's right).

0 is called the null pointer constant, and when compared to or assigned to another pointer, it is converted to a null pointer of the same type.

# 23.4 Pointers as Integers

You can cast pointers to integers and vice-versa (since a pointer is just an index into memory), but you only ever need to do this if you're doing some low-level hardware stuff. The results of such machinations are implementation-defined, so they aren't so. And *weird* things could happen.

> This will vary depending on the architecture, but my system is little endian, which means the least-significant byte of the number is stored first. Big endian systems will have the 12 first and the 78 last. But the spec doesn't dictate anything about this representation.
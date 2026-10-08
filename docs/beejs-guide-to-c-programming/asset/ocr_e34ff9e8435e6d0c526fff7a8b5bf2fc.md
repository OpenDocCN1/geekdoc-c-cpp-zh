```
fp = fopen("output.bin", "rb"); // rb for "read binary!"
```

```
while (fread(&c, sizeof(char), 1, fp) > 0)
    printf("%d\n", c);
```

And, running it, we see our original numbers!

+   5
37
0
88
255
12

Woo hoo!

# 9.6.1 struct and Number Caveats

As we saw in the structs, the compiler is free to add padding to a struct as it sees fit. Different compilers might do this differently. And the same compiler on different architectures could do it differently. And the same compiler on the same architectures could do it differently.

What I'm getting at this is: it's not portable to fwrite() an entire struct to a file when you don't know where the padding will end up.

How do we fix this? Hold that thought—we'll look at some ways to do this after looking at another related problem.

Numbers!

Turns out all architectures don't represent numbers in memory the same way.

Let's look at a simple fwrite(v) of a 2-byte number. We will write it in hex so by byte. The most significant byte will have the value 0x12 and the least significant will have the value 0x34.

```
unsigned short v = 0x1234; // Two bytes, 0x12 and 0x34
```

```
fwrite(&v, sizeof(v), 1, fp);
```

What ends up in the stream?

Well, it seems like it should be 0x12 followed by 0x34, right?

But if I is not on my machine and he dumps the result, I get:

34 12

They're reversed! What gives?

This has something to do with what's called the endianness of the architecture. Some write the most significant bytes first, and some the least significant bytes first.

This means that if you write a multibyte number out from memory, you can't do it in a portable way⁶.

A similar problem exists with floating point. Most systems use the same format for their floating point numbers, but some do not. No guarantees!

So... how can we fix all these problems with numbers and structs to get our data written in a portable way?

> ⁵https://en.wikipedia.org/wiki/Endianness

> ⁶And this is why I used individual bytes in my fwrite() and fread() examples, above, shrewdly.
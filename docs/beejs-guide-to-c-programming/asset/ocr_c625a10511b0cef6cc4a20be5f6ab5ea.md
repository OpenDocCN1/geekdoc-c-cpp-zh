```
struct foo {
    unsigned int a:1;
    unsigned int b:2;
    unsigned int c:3;
    unsigned int d:4;
};
```

the compiler packs all these into a single unsigned int. But what if you needed a and b in int, and c and d in a different one?

There's a solution for that: put an unsigned bit-field of width where you want the compiler to start anew with packing bits in a different int:

```
struct foo {
    unsigned int a:1;
    unsigned int b:2;
    unsigned int :0; // <--Zero-width unnamed bit-field
    unsigned int c:3;
    unsigned int d:4;
};
```

It's analogous to an explicit page break in a word processor. You're telling the compiler, "Stop packing in unsigned, and start packing them in the next one."

By adding the zero-width unnamed bit field in that spot, the compiler puts a and b in one unsigned int, and c and d in another unsigned int. Total, for a size of 8 bytes on my system (unsigned ints are 4 bytes each).

# 20.9 Unions

These are basically like structs, except the fields overlap in memory. The union will be large enough for the largest field, and you can use only one field at a time.

It's a way to reuse the same memory space for different types of data.

You declare them just like structs, except it's union. Take a look at this:

```
union foo {
    int a, b, c, d, e, f;
    float g, h;
    char i, j, k, l;
};
```

Now, that's a lot of fields. If this was a struct, my system would tell me it took 36 bytes to hold it all. The biggest one is int (or float), taking up 4 bytes on my system. And, indeed, if for the sizeof the union foo, it tells me 4! The tradeoff is that you can only use one of fields at a time. However...

# 20.9.1 Unions and Type Punning

You can non-portably write to one union field and read from another!
Doing so is type pun², and you'd use it if you really knew what you were doing, typically with some kind of low-level programming.

> https://en.en.wikipedia.org/wiki/Type_punning
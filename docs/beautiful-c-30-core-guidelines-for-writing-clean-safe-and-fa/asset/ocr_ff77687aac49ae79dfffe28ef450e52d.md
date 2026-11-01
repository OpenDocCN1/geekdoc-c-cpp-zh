Indeed, if you add a third bool after m_b2 thus:

Click here to view code image

```
struct int_two_bools {
    bool m_b1;
    bool m_b2;
    bool m_b3;
    int m_i;
};
```

you STILL get the answer 8.

![](bbox=[0.13, 0.52, 0.38, 0.62])

Figure 2.4.3. Optimized layout for storing an integer and three bools

This may come as a surprise. The standard has a few things to say about alignment, which you can find at [basic.align].¹ In summary, individual objects must be aligned on boundaries matching their size. In this example, and for this implementation, sizeof(bool) is 1 and sizeof(int) is 4. In the first definition of int_two_bools, the first bool member occupies one byte. Three bytes of padding are then added so that the int member will lie on a four-byte boundary. In the second definition, the two bool members are consecutive and only need to be aligned on a one-byte boundary. This means that only two bytes of padding are required before the int member. In the third definition, only a single byte of padding is required since all three bool members can fit in four bytes.

1. https://eel.is/c++draft/basic.align

This demonstrates that layout order is significant with regard to the size of an instance of a class. This is particularly relevant if you are in a size-constrained situation and have a million objects: those extra four bytes may be very valuable. Solving initialization order problems may not be as
The next part, setting the lines in anti-phase, isn't so simple. The obvious approach is:

```
int main() {
    volatile unsigned int *dirset=(unsigned int*)(0x500000000UL+0x518);
    volatile unsigned int *outset=(unsigned int*)(0x500000000UL+0x508);
    volatile unsigned int *outclr=(unsigned int*)(0x500000000UL+0x50C);

    volatile int i;
    int n = 200;
    unsigned int mask = 1 << 3 | 1 << 2;
    unsigned int mask1 = 1 << 3;
    unsigned int mask2 = 1 << 2;
    *dirset = mask;
    for (;;) {
        *outset = mask1;
        *outclr = mask2;
        for (i = 0; i < n; i++) {
            *outclr = mask1;
            *outset = mask2;
            for (i = 0; i < n; i++) {
            }
        }
    }
}}
```

In this case we set P0 and P1 in separate operations so they are switched at slightly different times.

If you look at a logic analyzer you will discover that there is a 0.25 µs V1 or 50 ns V2 overlap:

| +300ns overlap | A1 | A2 | 00ns |
|---|---|---|---|n| Measurements | | | |
| Width: 47.45us | | | |
| Period: 94.95us DutyCycle: 50.0263296% Frequency: 10.5318589KHz |
| Pulse Counters | | | |
| Timing Marker Places | | | |
| A1 - A2 | =50ns A1 @ 117.76735ms A2 @ 117.7764ms | | |
| Analyzers | | | |
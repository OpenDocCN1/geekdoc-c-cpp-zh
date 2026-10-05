# D.2. THE FLOATING-POINT TYPES

binary point. The base of the exponent is, of course, two, and a 2-bit exponent is used. D.4 illustrates such a value. For simplicity, neither the mantissa nor the exponent is negative. Thus, the mantissa ranges

![](bbox=[0.355, 0.19, 0.685, 0.28])

Figure D.4: Simplified exponential value

```
$$(1 \times 2^{-1} + 0 \times 2^{-2} + 1 \times 2^{-3}) \times 2^{(1\times 2^{-1}+0\times 2^{-2})} = (\frac{1}{2} + \frac{1}{8}) \times 2^2 = \frac{5}{8} \times 4 = 2.5$$
```

The range of these abbreviated floating-point numbers is $0\dots7$. This range is misleading, however, since it leaves the impression that any value could be represented. 2.5 can be represented in this scheme, but 2.4 *cannot*. This floating-point scheme is so simple that we can easily enumerate all the possible values, as Table D.2.

| Mantissa Values | Exponent Values | | | | |
|--- | --- | --- | --- | --- | --- |
| .000 (0) | $00$ ($0$) | $01$ ($1$) | $10$ ($2$) | $11$ ($3$) | $2^3 (8) |
| .001 (0.125) | 0.125 | 0.25 | 0.5 | 1 |
| .010 (0.25) | 0.25 | 0.5 | 1 | 2 |
| .011 (0.375) | 0.375 | 0.75 | 1.5 | 3 |
| .100 (0.5) | 0.5 | 1.25 | 2.5 | 4 |
| .101 (0.625) | 0.625 | 1.5 | 3 | 6 |
| .110 (0.75) | 0.75 | 1.75 | 3.5 | 7 |
| .111 (0.875) | 0.875 | 1.75 | | | |

Table D.2: A complete enumeration of our simplified floating-point numbers. Decimal equivalents appear in parenthe-

s-ses.

Figure D.5 plots these values on the real number line.

Table D.2 and Figure D.5 reveal several troubling issues:

+   1. There are many gaps; for example, the value 2.4 is missing and cannot be represented exactly
(2.5 is the closest approximation).
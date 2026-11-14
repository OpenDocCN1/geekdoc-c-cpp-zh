```
/* Reflect the next byte in the message,
 * then shift and XOR with the
 * remainder. */
reflection =
    (uint16_t) reflect8(p_data[byte]);
remainder ^= (uint16_t) reflection << 8;
/* Bit-by-bit division, modulo 2. */
for (int bit = 8; 0 < bit; --bit)
{
    remainder <<= 1;
    if (0U != (remainder & CRC16_MSB))
    {
        remainder ^= CRC16_POLY;
    }
}
/* Reflect the result. Some CRC variants also
 * add an additional XOR at the end. */
return reflect16(remainder);
}
```

Fig 6.3 - Cyclic redundancy checks are widely used for data verification and provide more reliable checking than LRC algorithms. Calculation is slow by comparison, although lookup tables of precomputed values are commonly used to improve performance.

Checksums are related to, and often considered to be, hash functions – a class of functions that map arbitrary amounts of data into a single, fixed-size value, sometimes referred to as a Such functions have a wide variety of uses – error detection being only one of them. Of particular interest in
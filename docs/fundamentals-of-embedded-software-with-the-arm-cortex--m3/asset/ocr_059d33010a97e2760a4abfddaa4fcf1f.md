![](bbox=[0.214, 0.086, 0.856, 0.303])

FIGURE 2-5 Interpreting a 2's-complement number based on its sign bit.

```
01110110₂ = 0x(-2⁷) + 1x2⁶ + 1x2⁵ + 1x2⁴ + 0x2³ + 1x2² + 1x2¹ + 0x2⁰
          = 64 + 32 + 16 + 4 + 2
          = 118₁₀

10100111₂ = 1x(-2⁷) + 0x2⁶ + 1x2⁵ + 0x2⁴ + 0x2³ + 1x2² + 1x2¹ + 1x2⁰
          = -128 + 32 + 4 + 2 + 1
          = -89₁₀
```

FIGURE 2-6 Modified polynomial evaluation of a 2's-complement number.

# 2.3.4 Changing the Sign of Numbers with Integer and Fractional Parts

When finding the 2's-complement representation of a signed decimal number, the usual approach is to first convert the positive equivalent to binary and then apply the 2's-complement algorithm to make it negative. A common mistake while converting a number that contains both integer and fractional parts is to treat the parts separately. For example, when converting the number -5.75₁₀ to an 8-bit 2's-complement representation with the binary point in the middle, you might be tempted to do it as follows:

+   Step 1: +5₁₀ = 0101, thus -5₁₀ becomes 1011
+   Step 2: .75₁₀ = .1100
+   Step 3: Combining yields 1011.1100₂

Unfortunately, this result corresponds to -4.25, not -5.75. The correct way of conversion is to first find the 8-bit representation of +3.75 and then apply the 2's-complement algorithm as if there was no binary point:
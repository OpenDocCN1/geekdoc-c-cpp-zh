to have the yet stronger lower estimate:

```
|λ_{l±2}| ≥ π² |(l ± 2)² - ((l ± 1)² + l²)/2| ≥ π² (3l - 7/2) ≥ π² l ≥ π² π⁻¹ √(-ℜ K / 2).
```

Clearly, even for the case l = 0 for which ||c^{(l)}|| is maximal, we still have

```
||p|| / ||α_l c^{(l±2)}|| = |α_l| ||c^{(l)} - c^{(l±2)}|| / ||α_l c^{(l±2)}|| = ||c^{(l)} - c^{(l±2)}|| / ||c^{(l±2)}|| = √[||c^{(l)}||² + ||c^{(l±2)}||²] / ||c^{(l±2)}|| ≤ √3.
```

Therefore,

```
||A p|| ≥ |λ_{l±2}| · |α_l| ||c^{(l±2)}|| ≥ |λ_{l±2}| ||p|| / √3,
```

or

```
||A p|| / ||p|| ≥ |λ_{l±2}| / √3.
```

By combining this inequality with the lower bound developed before for |λ_{l±2}|, we have the required lower bound for ||A p|| / ||p|| as well. The inverse of this lower bound provides the required upper bound for ||A⁻¹||.

As a result, the above error estimate simplifies to read

```
||error|| ≤ (√3 / 30π²) |K|² h² + O(|K|³ h⁴).
```

Furthermore, if

```
-ℜ K > (5π)² / 2,
```

then the error estimate can improve to read

```
||error|| ≤ (√6 / 12π) |ℜ K|⁻¹ᐟ² |K|² h² + O(|ℜ K|⁻¹ᐟ² |K|³ h⁴).
```

# 25.7 Adequacy

The above analysis still holds even in the more practical case in which |K| → ∞ as h → 0, provided that

```
K ≪ h⁻².
```

Thus, the above error estimates are still valid, which means that the finite-difference scheme is adequate in the sense of [67].
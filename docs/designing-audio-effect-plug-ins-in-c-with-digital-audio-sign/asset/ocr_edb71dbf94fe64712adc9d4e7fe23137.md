inspection.

> When the denominator of the transfer function is zero, the output is infinite. The complex frequency where this occurs is the pole frequency or pole.

Examining the transfer function, we can find the single pole in Equation 5.40:

```
H(z) = a_0 \frac{1}{1 + b_1 z^{-1}}
= a_0 \frac{1}{1 + \frac{b_1}{z}}
= a_0 \frac{z}{z + b_1}
(5.40)
```

By rearranging the transfer function, you can see that the denominator will be zero when \(z = -b_1\) and so there is a pole at \(z = -b_1\). You might also notice something interesting about this transfer function— it has a \(z\) in the numerator. If \(z = 0\), then this transfer function has a zero at \(z = 0\). This zero is called a trivial zero because it has no impact on the filter’s frequency response. Thus, you can ignore the zero at \(z = 0\). In fact, you can also ignore poles at \(z = 0\) for the same reason.

And, if you look back at the transfer function in the feed-forward filter in Equation 5.35 you can see that it also had a pole in Equation 5.41:

```
H(z) = a_0 [1 + \alpha_1 z^{-1}]
= a_0 [1 + \frac{\alpha_1}{z}]
(5.41)
Pole at \(z = 0\)
```

The poles are plotted in the z-plane in the same manner as the zeros but you use an x to indicate the pole frequency. In Equation 5.40, the pole is at \(-b_1 + j0\) and so it is a real pole located on the real axis in the z-plane. For this filter let’s analyze it with \(a_0 = 1.0\) and \(b_1 = 0.9\). You wrote a plug-in and implemented this filter in the last chapter. The results are shown in Figure 5.27.

Let’s see how this is estimated first, and then we can do a direct evaluation as before.

# Step 4: Estimate the frequency response

The single pole is plotted on the real axis at \(z = -0.9 + j0\) and a trivial zero at \(z = 0 + j0\) (Figure 5.28). In the future, we will ignore the trivial zeros or poles.

> A pole or zero at \(z = 0\) is trivial and can be ignored for the sake of analysis since it has no effect on the frequency response.
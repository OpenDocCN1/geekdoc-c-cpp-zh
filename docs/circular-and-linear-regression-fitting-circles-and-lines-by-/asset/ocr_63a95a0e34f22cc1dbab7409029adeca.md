The Pratt and Taubin fits are more easily expressed in terms of the algebraic circle parameters $A, B, C, D$, in which the circle is defined by equation

```
$Az+Bx+Cy+D=0, \quad \text{where} \quad z=x^2+y^2\,.$
```

Now the limit point of the Pratt fit satisfies

```
$$(A^{*}, B^{*}, C^{*}, D^{*})=\operatorname{argmin}\,\int [Az+Bx+Cy+D]^2\, d\mathbb{P}\sigma \qquad (7.55)$$
```

subject to the constraint

```
$$B^2+C^2-4AD=1. \qquad (7.56)$$
```

The limit point of the Taubin fit, see (5.49)–(5.51), is obtained by minimizing the same integral (7.55), but subject to $two$ constraints: one is $(7.56)$ and the other is

```
$$\int (Az+Bx+Cy+D)\, d\mathbb{P}=0,$$
```

see Section 5.9. That additional constraint makes the limit point $(A_{\mathrm{T}}^{*}, B_{\mathrm{T}}^{*}, C_{\mathrm{T}}^{*}, D_{\mathrm{T}}^{*})$ of the Taubin fit different from that of Pratt, $(A_{\mathrm{P}}^{*}, B_{\mathrm{P}}^{*}, C_{\mathrm{P}}^{*}, D_{\mathrm{P}}^{*})$.

After determining the limit points $(A^{*}, B^{*}, C^{*}, D^{*})$ for the Pratt and Taubin fits we can apply the conversion formulas $(3.11)$ to find the corresponding limit values $(a^{*}, b^{*}, R^{*})$. We omit analytical derivation and present the final results below.

The “hyperaccurate” circle fit developed in Section 7.5 cannot be expressed in the form $(6.44)$, so we leave it out of our analysis.

**Approximate limit points for circular fits.** We give the limit points $(a^{*}, b^{*}, R^{*})$ for all our circle fits approximately, to the leading order in $\sigma$. We assume, as Berman [17] did, that the measure $\mathbb{P}_{0}$ describing the distribution of the true points is either uniform on the entire circle or uniform on an arc of length $\theta < 2\pi$.

Now in both cases the geometric radius estimate satisfies

```
$$R_{\mathrm{G}}^{*}=R+\frac{\sigma^{2}}{2 R}+\mathcal{O}\left(\sigma^{3}\right)$$
```

(note that it is independent of $\theta$). This formula remarkably agrees with our early expression $(7.11)$ for the essential bias of the geometric fit. The Taubin estimate is

```
$$R_{\mathrm{T}}^{*}=R+\frac{\sigma^{2}}{R}+\mathcal{O}\left(\sigma^{3}\right),$$
```

i.e., its asymptotic bias is twice as large, to the leading order. The Pratt limit radius estimate is

```
$$R_{\mathrm{P}}^{*}=R+\frac{2\sigma^{2}}{R}+\mathcal{O}\left(\sigma^{3}\right),$$
```
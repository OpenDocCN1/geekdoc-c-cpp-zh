which suggest that

$A_2 = \overline{x^2} - \sigma^2,\quad \quad B_2 = \overline{x^2 y} - \bar{y}\sigma^2$,  
$A_3 = \overline{x^3} - 3\bar{x}\sigma^2,\quad \quad B_3 = \overline{x^3 y} - 3\overline{xy}\sigma^2$,  
$A_4 = \overline{x^4} - 6\overline{x^2}\sigma^2 + 3\sigma^4,\quad B_4 = \overline{x^4 y} - 6x^2y\sigma^2 + 3\bar{y}\sigma^4$.

This method can be directly extended to arbitrary $A_m$ and $B_m$, see [30] and Section 6.4 in [40].

Lastly, the adjusted least squares estimates are the solutions of the system

$\beta_0A_m + \beta_1 A_{m+1} + \cdots + \beta_k A_{m+k} = B_m,\quad\quad m = 0, \dots, k \quad\quad\quad\quad (6.52)$

**Adjustments for implicit nonlinear models.** This section covered explicit functional relations — linear and polynomial models. In most computer vision applications, though, one fits implicit nonlinear models to data; see Section 1.9. Those require more sophisticated approaches, discussed further in Section 7.8.
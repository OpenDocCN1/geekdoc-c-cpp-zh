# j = 10, n = 10

# j = 10, n = 30

# j = 10, n = 100

![](bbox=[0.1, 0.18, 0.86, 0.65])

FIGURE 4. Plots of the magnitudes of the matrix entries in the j = 10th column of A_n(f)^ and G_n(f)^, with n = 10, 30, 100, for Example 2. For small n, the amplitude of G_n(f)^_kj is similar to that of A_n(f)^_kj, indicating that little cancellation has occurred. By the time n reaches 100, the leading 90 digits of A_n(f)^_kj have been eliminated in the recurrence (3.14) to obtain G_n(f)^_kj for typical values of j, k.

self-adjointness of each G_n(f)^. This is done by measuring

```
(3.22) r_n = max_{j,k∈K} |G_n(f)^_kj - overline{G_n(f)^_jk}| / ||G_n(f)^||_F , K = {k : |k| < K/2}.
```

In Figure 6, we plot r_n versus n for each of the three examples. Note that 300 bits of precision was not sufficient in the unfiltered case of Example 1 to avoid O(1) errors in the symmetry of G_n(f)^, whereas 600 bits gives at least 90 correct
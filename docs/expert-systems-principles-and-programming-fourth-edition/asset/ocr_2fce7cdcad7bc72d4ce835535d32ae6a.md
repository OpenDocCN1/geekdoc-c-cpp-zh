+   • dilution:

```
DIL (A)
```

```
μ_DIL(A) (x) = (μ_A (x))^0.5
```

The DIL operation dilates fuzzy elements by increasing the membership grade more of elements with smaller membership grades. Figure 5.14 illustrates DIL.

# Figure 5.14 Dilation of a Fuzzy Set

![](bbox=[0.223, 0.26, 0.933, 0.41])

Notice that it performs the inverse operation to concentration for these choices of powers 2 and 0.5:

```
A = DIL (CON (A)) = CON (DIL (A))
```

The dilation operator is roughly approximated by the linguistic modifier More Or Less. Thus for any fuzzy set F:

```
More Or Less F = F^0.5 = DIL (F)
```

+   • intensification:

# INT (A)

```
μ_INT(A)(x) = { 2 (μ_A(x))^2 for 0 ≤ μ_A(x) ≤ 0.5; 1 - 2(1 - μ_A(x))^2 for 0.5 ≤ μ_A(x) ≤ 1 }
```

The INT operation is like contrast intensification of a picture. As illustrated in Figure 5.15, the intensification raises the membership grade of those elements within the crossover points and reduces the membership grade of those outside the crossover points. As an electronic analogy, consider the crossover points as defining the bandwidth of a signal. Intensification amplifies the signal within the bandwidth while reducing the "noise" outside the bandwidth. Intensification thus increases the contrast in grade between those elements within the crossover points compared to those outside the crossover points.
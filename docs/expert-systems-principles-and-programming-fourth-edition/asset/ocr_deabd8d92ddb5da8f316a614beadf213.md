which means that the likelihood of our belief is 38.2% that SMIR is true.

What we really need is the probability of the HYPE hypothesis based on the uncertain evidence of SMIR, which is P(HYPE | RCIB). One way of calculating this uses the formula for P(H | e) discussed in Section 4.14 as:

```
P(H | e) = {
    P(H | E') + (P(H) - P(H | E')) * P(E | e') / P(E)
    for 0 <= P(E | e) < P(E)
    P(H) + (P(H | E) - P(H)) * (P(E | e) - P(E)) / (1 - P(E))
    for P(E) <= P(E | e) <= 1
}
```

where the uncertainty in the SMIR evidence is:

```
P(E | e) = P(SMIR | RCIB) = 0.382
```

and the probability we want is:

```
P(H | e) = P(HYPE | SMIR)
```

where all we know is:

```
P(H | E) = (O(H | E)) / (1 + O(H | E)) = 3.00 / (1 + 3.00) = 0.75
```

and the prior odds from Figure 4.19 are:

```
P(H) = P(HYPE) = 0.01
```

```
P(E) = P(SMIR) = 0.03
```

Since P(E | e) > P(E), we will use the formula for P(E) <= P(E | e) <= 1 to compute P(H | E) as follows:

```
P(H | e) = 0.01 + ((0.75 - 0.01)(0.382 - 0.03)) / (1 - 0.03)
```

```
P(HYPE | RCIB) = 0.279
```

which is the posterior probability of HYPE.

This propagation of probabilities continues up the inference net. Now the probability P(HYPE | RCIB) is the uncertain evidence of FLE. The posterior probability P(FLE | RCIB) is calculated using the same formula with values adjusted for FLE:
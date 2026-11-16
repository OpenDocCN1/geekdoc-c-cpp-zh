Based on the above equation, we can clearly distinguish two distinct conditional expectations given the events A12 and A22. According to the analysis done at the beginning of this subsection, these conditional expectations can be established as

```
E \left( D \mid A_{12}, (c = j) \right) = E \left( DC_1 \mid c = j \right) \quad (14.21)

E \left( D \mid A_{22}, (c = j) \right) = E \left( DC_2 \mid c = j \right) \quad (14.22)
```

where DC1 and DC2 are the random variables describing the detection delay when (A12 = L overlaps \(\lceil \frac{L}{T} \rceil\) cycles) and (A22 = L overlaps \(\lceil \frac{L}{T_s} \rceil + 1\) cycles), respectively. More specifically, DC1 and DC2 can be written as

```
DC_1 = \left( \lambda x . \left( x - \frac{3}{2} + \frac{s}{2} \right) \times T \right) \circ DR_1 \quad (14.23)

DC_2 = \left( \lambda x . \left( x - 2 + \frac{s}{2} \right) \times T \right) \circ DR_2 \quad (14.24)
```

where the \(\circ\) operator denotes the function composition, and DR1 and DR2 are the delay round random variables given A12 and A22, respectively, as described above Plugging the above two equations, into Equations (14.21) and (14.22), and applying the conditional expectation of a function of a random variable, we derive, from Equation (14.25), that the conditional expectation of D given (c = j), E (D | c = j), equals

```
(1-s) \times \sum_{i=2}^{ph1} \left( i - \frac{3}{2} + \frac{s}{2} \right) \times T \times P_r \left( DR1 = i \mid A_{12} \cap (c = j) \right) +

s \times \sum_{i=2}^{ph2} \left( i - 2 + \frac{s}{2} \right) \times T \times P_r \left( DR2 = i \mid A_{22} \cap (c = j) \right) \quad (14.25)
```

Now, analyzing the relationship between the random variables, we can establish that DR1 and IT are conditionally independent given the random variable c. Indeed, in terms of events, the information A12 does not add anything about (DR1 = i) if we already know that (c = j). Similarly for (DR2 = i) and A22 given(c = j). Now, we can simplify Equation (14.25) into
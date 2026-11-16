For our die, the events of an even number and a number divisible by three definitely affect each other and so is not a stochastic experiment. The probability of an even number on one die and a number divisible by three on another is stochastic.

```
P(A U B) = P(A) P(B) = 3/6 . 2/6 = 1/6
```

Now let's consider the case of the union of events, P(A U B). Define n as a function that returns the number of elements of a set. If we add the number of elements in A to those in B and divide by the total elements in the sample space n(S),

```
(1) P(A U B) = n(A) + n(B) / n(S) = P(A) + P(B)
```

then the result will be too big if the sets overlap. If you look at Figure 4.5, applying this formula gives:

```
P(A U B) = 3 + 2 / 6 = 5 / 6
```

but you can easily see that there are only four elements in the union since:

```
A U B = { 2, 3, 4, 6 }
```

The problem is that just adding n(A) to n(B) is counting the set intersection {6} twice since it belongs to both A and B.

The correct formula simply requires subtracting the extra probability of set intersection:

```
(2) P(A U B) = P(A) + P(B) - P(A n B)
```

which for our die reduces to:

```
P(A U B) = 3/6 + 2/6 - 1/6 = 4/6 = 2/3
```

Formula (1) holds when the sets are disjoint and so have no elements in common. It is a special case of formula (2), which is called the Additive Law. The Additive Law can also be derived as a theorem using the three axioms of probability discussed earlier. The Additive Law for three events is:

```
P(A U B U C) = P(A) + P(B) + P(C)
- P(A n B) - P(A n C) - P(B n C)
+ P(A n B n C)
```

Other laws for neither A nor B and the exclusive-OR of A and B can also be
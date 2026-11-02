And how many iterations do we make? We need to swap all coins in the first half. That is, we need to swap size / 2 coins. The pseudocode is

```
i = 0
j = size / 2
While i < size / 2
Swap elements at positions i and j
i++
j++
```

You can use paper clips as position markers or counters.

It is a good idea to make a walkthrough of the pseudocode (see Section 4.2). You can use paper clips to denote the positions of the variables i and j. If the walkthrough is successful, then we know that there was no "off-by-one" error in the pseudocode. Exercise E6.6 asks you to translate the pseudocode to C++. Exercise R6.19 suggests a different algorithm for switching the two halves of an array, by repeatedly removing and inserting coins.

Many people find that the manipulation of physical objects is less intimidating than drawing diagrams or mentally envisioning algorithms. Give it a try when you need to design a new algorithm!

# 6.6 Two-Dimensional Arrays

It often happens that you want to store collections of values that have a two-dimensional layout. Such data sets commonly occur in financial and scientific applications. An arrangement consisting of rows and columns of values is called a two-dimensional array, or a matrix.

![](bbox=[0.52, 0.68, 0.9, 0.85])

Let's explore how to store the example data shown in Figure 10: the medal counts of the figure skating competitions at the 2014 Winter Olympics.

![](bbox=[0.22, 0.78, 0.33, 0.92])

| Country | Gold | Silver | Bronze |
|---|---|---|---|
| Canada | 0 | 3 | 0 |
| Italy | 0 | 0 | 1 |
| Germany | 0 | 0 | 1 |
| Japan | 1 | 0 | 0 |
| Kazakhstan | 0 | 0 | 1 |
| Russia | 3 | 1 | 1 |
| South Korea | 0 | 1 | 0 |
| United States | 1 | 0 | 1 |

Figure 10 Figure Skating Medal Counts
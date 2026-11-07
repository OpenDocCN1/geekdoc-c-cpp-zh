# ## Anscombe’s Quartet

An important step in data analytics is “getting to know your data.” The *basic descriptive statistics* above certainly help you know more about your data. One caution, though, is that dramatically different datasets actually can have identical or nearly identical descriptive statistics. For an example of this phenomenon, we’ll consider *Anscombe’s Quartet*.

https://en.wikipedia.org/wiki/Anscombe%27s_quartet

Anscombe’s Quartet consists of the following four sets of *x-y* coordinate pairs with 11 data samples each:

| x1 | y1 | x2 | y2 | x3 | y3 | x4 | y4 |
|---:|---:|---:|---:|---:|---:|---:|---:|
| 10.0 | 8.04 | 10.0 | 9.14 | 10.0 | 7.46 | 8.0 | 6.58 |
| 8.0 | 6.95 | 8.0 | 8.14 | 8.0 | 6.77 | 8.0 | 5.76 |
| 13.0 | 7.58 | 13.0 | 8.74 | 13.0 | 12.74 | 8.0 | 7.71 |
| 9.0 | 8.81 | 9.0 | 8.77 | 9.0 | 7.11 | 8.0 | 8.84 |
| 11.0 | 8.33 | 11.0 | 9.26 | 11.0 | 7.81 | 8.0 | 8.47 |
| 14.0 | 9.96 | 14.0 | 8.10 | 14.0 | 8.84 | 8.0 | 7.04 |
| 6.0 | 7.24 | 6.0 | 6.13 | 6.0 | 6.08 | 8.0 | 5.25 |
| 4.0 | 4.26 | 4.0 | 3.10 | 4.0 | 5.39 | 19.0 | 12.50 |
| 12.0 | 10.84 | 12.0 | 9.13 | 12.0 | 8.15 | 8.0 | 5.56 |
| 7.0 | 4.82 | 7.0 | 7.26 | 7.0 | 6.42 | 8.0 | 7.91 |
| 5.0 | 5.68 | 5.0 | 4.74 | 5.0 | 5.73 | 8.0 | 6.89 |

Interestingly, these datasets have *nearly identical* descriptive statistics. For instance, in all four datasets, the *x*- and *y-coordinates’* mean values are 9 and 7.5, respectively.

The following diagrams—which our fully coded *case study* example creates—plot the *x1-y1*, *x2-y2*, *x3-y3* and *x4-y4* data, respectively:

![](bbox=[0.172, 0.64, 0.827, 0.946])
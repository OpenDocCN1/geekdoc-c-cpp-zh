PDOC    Number of doctorates who got postdoctoral training.

The aim is to estimate a logit model predicting the probability that a doctorate will receive postdoctoral training.

Here’s the SAS code to read in the data:

```
DATA nihdoc;
    INPUT nih docs pdoc;
    DATALINES;
.5 8 1
.5 9 3
.835 16 1
.998 13 6
1.027 8 2
2.036 9 2
2.106 29 10
2.329 5 2
2.523 7 5
2.524 8 4
2.874 7 4
3.898 7 5
4.118 10 4
4.130 5 1
4.145 6 3
4.242 7 2
4.280 9 4
4.524 6 1
4.858 5 2
4.893 7 2
4.944 5 4
5.279 5 1
5.548 6 3
5.974 5 4
6.733 6 5
7 12 5
9.115 6 2
9.684 5 3
12.154 8 5
13.059 5 3
13.111 10 8
13.197 7 4
13.433 86 33
13.749 12 7
14.367 29 21
14.698 19 5
```
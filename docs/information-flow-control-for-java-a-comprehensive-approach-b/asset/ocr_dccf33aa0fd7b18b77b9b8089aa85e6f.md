# CHAPTER 5. PATH CONDITIONS

```
1 LINE 1
2 USE a_2 2
3 DEF x_1 2
4 LINE 2
5 USE x_3 2
6 LINE 3
7 USE y_5 2
8 USE x_6 2
9 DEF x_4 4
10 LINE 4
11 USE x_7 2
12 LINE 2
13 USE x_3 4
14 LINE 3
15 USE y_5 2
16 USE x_4 4
17 DEF x_4 6
18 LINE 4
19 USE x_7 6
20 LINE 2
21 USE x_3 6
22 LINE 3
23 USE y_5 2
24 USE x_6 6
25 DEF x_4 8
26 LINE 4
27 USE x_7 8
28 LINE 5
29 USE x_8 8
30 LINE 2
31 USE x_3 8
```

Figure 5.10: A simple program trace along with their respective node numbers as Figure 5.2

for the program trace to list variables with their respective node numbers as in Figure 5.10 which shows a simple trace for a run of the program from Figure 5.2.

Note that the node numbers are different to the SSA-numbers from Figure 5.2 and thus, the path condition for a flow from line 1 to 5 is PC(1,5) = (x_3 < 7) \wedge (x_7 = 8). For this path condition the trace yields the variable assignments

```
$R = (x_3 = 2 \vee x_3 = 4 \vee x_3 = 6) \wedge (x_7 = 4 \vee x_7 = 6) \vee (x_7 = 8)$
```

Again, both clauses are conjunctively combined to $PC' = PC \wedge R$ yielding the stronger and more precise path condition $PC'$.

```
$PC' = (x_3 = 2 \vee x_3 = 4 \vee x_3 = 6) \wedge (x_7 = 8)$
```
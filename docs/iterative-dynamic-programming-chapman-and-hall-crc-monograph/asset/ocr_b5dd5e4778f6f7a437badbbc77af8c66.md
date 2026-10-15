![](bbox=[0.35, 0.08, 0.65, 0.37])

Figure 11.17: Optimal control policy with P = 48 for Example 7

with

```
g₁ = (0.11 x₃) / (0.006 x₁ + x₃)    (11.138)
```

```
g₂ = (0.0055 x₃) / (0.0001 + x₃(1 + 10 x₃))    (11.139)
```

The initial state is

```
x(0) = [1.5  0  0  7]ᵀ.    (11.140)
```

The constraints on the feed rate are

```
0 ≤ u ≤ 50,    (11.141)
```

and on the state variables are

```
0 ≤ x₁ ≤ 40    (11.142)
```

```
0 ≤ x₃ ≤ 25    (11.143)
```

```
x₄(t_f) − 10 = 0    (11.144)
```

where t_f is the batch time. The performance index to be maximized is the total amount of penicillin produced at time t_f, given by

```
I = x₂(t_f) x₄(t_f).    (11.145)
```

The optimal control problem is to find the batch time t_f and the control policy u(t) in the time interval 0 ≤ t < t_f so that the performance index given in Eq. (11.145) is
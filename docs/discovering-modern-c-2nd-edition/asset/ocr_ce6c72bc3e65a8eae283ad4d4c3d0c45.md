![](bbox=[0.132, 0.092, 0.835, 0.423])

Figure 4–8: Simulated share price over 20 years

We hope that this introduction to random numbers will give you a smooth start to the exploration of this powerful library.

# 4.2.3 Mathematical Special Functions

C++17 C++17 introduced special mathematical functions that are summarized in Table 4–4. These functions are available for double values (function name as in table), for float (with suffix f), and for long double (with suffix l).

Table 4–4: Mathematical special functions

| Name | Precond. | Result |
|---|---|---|
| assoc_laguerr e(n, m, x) | for x >= 0 | L_n^m(x) = (-1)^m d^m/dx^m L_{n+m}(x) |
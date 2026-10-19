```
def func(x):
    return 5*(sin(8*x))**2*exp(-x*x)-13*cos(3*x)
def trapezoid(A,B,N):
    h = (B - A)/(N - 1)  # step size
    sum = (func(A)+func(B))/2  # (1st + last)/2
    for i in range(1, N-1):
        sum += func(A+i*h)
    return h*sum
A = 0.5
B = 2.3
N = 1200
print(trapezoid(A,B,N-1))
```

# 5.9 Algorithm: Trapezoid Rule

Trapezoid and Simpson integration rules use evenly spaced values of x (Figure 5.3). They use N points x_i(i = 1,N) evenly spaced a distance h apart throughout the integration region [a, b] and include the endpoints in the integration region. This means that there are (N − 1) intervals of length h:

h = (b - a)/(N - 1) , x_i = a + (i - 1)h , i = 1, N , (5.30)

where we start our counting at i = 1. The trapezoid rule takes each integration interval i and constructs a trapezoid of width h in it (Figure 5.3). This approximates f(x) by a straight line in each interval i and uses the average height (f_i + f_{i+1})/2 as the value for f. The area of each such trapezoid is

∫_{x_i}^{x_i+h} f(x) dx ≈ h(f_i + f_{i+1})/2 = 1/2 h f_i + 1/2 h f_{i+1} . (5.31)

![](bbox=[0.05, 0.82, 0.95, 0.98])
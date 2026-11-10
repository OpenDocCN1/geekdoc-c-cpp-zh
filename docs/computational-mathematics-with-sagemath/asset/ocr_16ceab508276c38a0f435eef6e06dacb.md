```
sage: y = function('y')(x)
sage: ed = (desolve(y*diff(y,x)/sqrt(1+y^2) == sin(x),y)); ed
sqrt(y(x)^2 + 1) == _C - cos(x)
```

The same problem appears. We impose that _C-cos(x) is positive:

```
sage: c = ed.variables()[0]
sage: assume(c-cos(x) > 0)
sage: sol = solve(ed,y) ; sol
[y(x) == -sqrt(_C^2 - 2*_C*cos(x) + cos(x)^2 - 1),
y(x) == sqrt(_C^2 - 2*_C*cos(x) + cos(x)^2 - 1)]
```

```
sage: P = Graphics()
sage: for j in [0,1]:
....:    for k in range(0,20,2):
....:        P += plot(sol[j].subsstitute(c==2+0.25*k).rhs(),x,-3,3)
sage: P
```

![](bbox=[0.353, 0.407, 0.703, 0.559])

2. Same method:

```
sage: sol = desolve(diff(y,x)==sin(x)/cos(y), y, show_method=True)
sage: sol
[sin(y(x)) == _C - cos(x), 'separable']
sage: solve(sol[0],y)
[y(x) == -arcsin(-_C + cos(x))]
```

**Exercise 40 page 222.** (Homogeneous equations) We verify that the equation $xy' = x^2 + y^2$ defined on $]0,+\infty[$ and on $]-\infty,0[$ is homogeneous, then we try to solve it by the change of unknown function indicated in the example treated in Section 10.1.2.

```
sage: x = var('x')
sage: y = function('y')(x)
sage: id(x) = x
sage: u = function('u')(x)
sage: D = diff(u*id,x)
sage: DE = (x*y*d == x*x+y*y).subsstitute(y == u*id)
sage: eq = desolve(DE,u)
```
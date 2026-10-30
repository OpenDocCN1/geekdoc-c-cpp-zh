# MODEL FORMULATION. Let

$x$ = ounces of Perfume #1 produced  
$y$ = ounces of Perfume #2 produced  
$z$ = ounces of main chemical purchased

Then

Maximize $P(x,y,z)=x\cdot(30-0.01x)+y\cdot(50-0.02y)-(3x+5y+10z)$  
subject to  
$x+y\le z$  
$z\le 1925$

Solution. Set up the model, define the Lagrangian function $L$, and use the techniques from the previous examples.

```
P := (x,y,z) -> x·(30 − 0.01x) + y·(50 − 0.02y) − (3x + 5y + 10z):
g1 := (x,y,z) -> x + y − z:
g2 := (x,y,z) -> z:
L := (x,y,z,λ1,λ2,μ1,μ2) -> P(x,y,z) + λ1·g1(x,y,z) + μ1² − 0.0
    + λ2·(g2(x,y,z) − 1925.0):
grad := Gradient(L(x,z,λ1,λ2,μ1,μ2), [x,y,z,λ1,λ2,μ1,μ2]):
vars := [x,y,z,λ1,λ2,μ1,μ2]:
NecessaryConditions := [seq(G = 0, G in grad)]:
    {NecessaryConditions};
    [
      27 − 0.02x + λ1 = 0
      45 − 0.04y + λ1 = 0
      −10 − λ1 + λ2 = 0
      μ1² + x + y − z = 0
      z + μ2² − 1925.0 = 0
    ]
```

Once again, we’re ready to begin working through the four cases. A summary of the results from Maple is shown in Table 4.9.
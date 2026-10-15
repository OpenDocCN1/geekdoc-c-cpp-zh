investigation of the viability of iterative dynamic programming by Luus and Smith [23] and for time-optimal control studies by Bojkov and Luus [4]. Here, based on that six-plate gas absorber model, we consider a more general case of an $n$-plate gas absorber controlled by inlet feed stream concentrations (see Figure 1.1). A material

![](bbox=[0.38, 0.19, 0.56, 0.6])

Figure 1.1: Gas absorber system consisting of $n$ equilibrium stages

balance around the $m$th plate of the absorption tower yields

```
$H\frac{dy_m}{dt}+h\frac{dx_m}{dt}=L(x_{m-1}-x_m)+G(y_{m+1}-y_m),\quad m=1,2,...,n,\qquad(1.44)$
```

where

+   - $x_m, y_m$ = composition of liquid and vapor leaving the $m$th plate (kg solute/kg inert),
+   - $h, H$ = inert liquid and vapor hold-ups on each plate (assumed constant) (kg),
+   - $L$ = flow rate of inert liquid absorbent (kg/min),
+   - $G$ = flow rate of inert gas stream (kg/min),
+   - $t$ = time of operation (min).

Expressing the flow rates in terms of inerts ensures that $L$ and $G$ remain constant from stage to stage, even though the physical flow rates change because of the absorption
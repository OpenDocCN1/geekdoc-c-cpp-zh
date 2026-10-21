The factor κ = cos(3α) is further evidence for the threefold rotational invariance of the Novikov–Veselov equations. Now we examine the Novikov–Veselov equation

```
u_t = -\frac{1}{4} u_{xx} + \frac{3}{4} u_{yy} + \frac{3}{4} \mathrm{div}(u \vec{v})
= -\frac{1}{4} n_1^3 u''' + \frac{3}{4} n_1^2 u'' + \frac{6}{4} n_1 u u' + \frac{3}{4} \beta u'
= -\frac{1}{4} \kappa u''' + \frac{6}{4} \kappa u u' + \frac{3}{4} \beta u'
```

Thus, a planar solution of the Novikov–Veselov equation has to be a solution of the KdV-like equation

```
\frac{4}{\kappa} u_t = -u''' + 6 u u' + \frac{3\beta}{\kappa} u'
```

The only essential modification is the contribution proportional to u' and thus it should not come as a surprise that the solutions are related. If q(t,s) is a solution of the standard KdV equation

```
\dot{q}(t,x) = -q''(t,x) + 6 q(t,x) q'(t,x)
```

then

u(t,s) = q(\frac{\kappa}{4} t, s + \frac{3\beta}{4} t)
is a solution of the Novikov–Veselov equation (1.2), which can be verified as follows:

```
u_t = \frac{\kappa}{4} q_t + \frac{3\beta}{4} q'
\frac{4}{\kappa} u_t + u''' - 6 u u' - \frac{3\beta}{\kappa} u' = q_t + \frac{3\beta}{\kappa} q' + q''' - 6 q q' - \frac{3\beta}{\kappa} q' = q_t + q''' - 6 q q' = 0
```

For a solution q(t,s) of KdV choose constants k_1 and k_2 with

```
\frac{3\beta}{4} = k_1 + k_2 \frac{3\kappa}{2}
```

and verify that

u(t,s) = q(\frac{\kappa}{4} t, s + k_1 t) - k_2
is a solution of the Novikov–Veselov equation:

```
u_t = \frac{\kappa}{4} q_t + k_1 q'
\frac{4}{\kappa} u_t + u''' - 6 u u' - \frac{3\beta}{\kappa} u' = q_t + \frac{k_1 4}{\kappa} q' + q''' - 6 (q - k_2) q' - \frac{3\beta}{\kappa} q' = q_t + q''' - 6 q q' + (\frac{k_1 4}{\kappa} + 6 k_2 - \frac{3\beta}{\kappa}) q' = q_t + q''' - 6 q q' + \frac{4}{\kappa} (k_1 + k_2 \frac{3\kappa}{2} - \frac{3\kappa}{4}) q' = 0
```

Remarks:

+   • Consider the choice β = k_1 = k_2 = 0. Then q(\frac{\kappa}{4} t, s) = u(\frac{\kappa}{4} t, s) is the KdV solution where the time scale is multiplied with κ/4. Since κ = κ(α) = cos(3α) the speed of the solution changes according to an angle dependent profile, as shown in Figure 1.
+   • The additive constant k_2 moves the KdV solution up or down in the graph.
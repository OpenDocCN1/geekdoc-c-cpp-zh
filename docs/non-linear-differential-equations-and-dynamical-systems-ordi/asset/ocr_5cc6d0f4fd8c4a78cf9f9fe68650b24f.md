# Unsteady, Non-Linear, and Chaotic Systems 245

where (II.7.124a) was used:

```
$d\left[\arc \tan \left(\frac{v}{u}\right)\right] = \frac{d(\frac{v}{u})}{1+(\frac{v}{u})^2} = \frac{\frac{dv}{u}-\frac{vdu}{u^2}}{1+\frac{v^2}{u^2}} = \frac{udv-vdu}{u^2+v^2}. \quad (4.491c)$
```

The index I coincides with the **winding number**; that is, the number of turns of the vector tangent to the integral curves as it describes the circle around the singularity, for example $I=2$ in Figure 4.33b.

# 4.9.6 Theorems of the Index and Winding Number

If there are several singularities or equilibrium points in a domain, their indices add to each other, as stated, more precisely in the **theorem of addition of indices**: the autonomous system (4.492a) has a continuously differentiable forcing vector that does not vanish (4.492c) on a closed curve $\partial D$, not in its interior, except (4.492b) possibly at a finite set of points $z_n$;

```
${{\dot{x},\dot{y}\}=\{u,v\}\in c^1(\mathbb{R}^2); \quad D-\partial D-\sum_{n=1}^N u^2+v^2\neq 0; \quad \sum_{n=1}^N I_n=\frac{[\theta]}{2\pi}. \quad (4.492a-d)$
```

then (problem 152) the sum of the indices of each point equals (4.492a) the index of the domain, is $1/2\pi$ the variation of the angle of the vector tangent to the integral curves around the boundary of the domain. It is sufficient to prove the theorem for two singular points (Figure 4.33c). The domain is divided by a curve AB joining the two boundaries and leaving one singularity on each side. The index of each singularity is (4.493a, b):

```
$2\piI_1=\int_{ADBA} d\theta;2\piI_2=\int_{ABCA} d\theta; \quad 2\pi(I_1+I_2)=\int_{ADB} d\theta+\int_{BA} d\theta+\int_{AB} d\theta, \quad (4.493a-c)$
```

and their sum is (4.493c). The integrals in AB in opposite directions cancel

```
$\int_{AB} d\theta=-\int_{BA} d\theta; \quad I_1+I_2=\frac{1}{2\pi}\int_{ADCA} d\theta=\int_{AD} d\theta=1, \quad (4.494a, b)$
```

and the remaining two in (4.494) add to the integral (4.494b) around the boundary. In particular if the boundary is a closed curve, the index is at least one, because there is at least one singularity or equilibrium point inside. The preceding theorems can be extended to the index (subsections 4.9.8) at the singularity at infinity (subsections 4.9.7).
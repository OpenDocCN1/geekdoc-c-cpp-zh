so that in normalized time all the time stages are of equal length

```
$$\tau_k = \frac{k}{P}, \quad k = 1, 2, \cdots, P.$$ (12.12)
```

The differential equation in the time interval $\tau_{k-1} \le \tau < \tau_k$ becomes

```
$$\frac{d\mathbf{x}}{d\tau} = v(k) P f(\mathbf{x}, \mathbf{u}).$$ (12.13)
```

With this transformation, at $t = t_f$, the transformed time variable $\tau = 1$, and the time to reach the desired state is

```
$$t_f = \sum_{k=1}^{P} v(k).$$ (12.14)
```

Minimization of the augmented performance index in Eq.(12.6) should give the minimum value to $t_f$ and ensure that the state variables at the final time are close to the desired values. In order to test the computational viability of this approach, we consider several examples. In all the examples we used the DVERK [7] subroutine, listed in Appendix E, to integrate the differential equations.

# 12.4 Examples

# 12.4.1 Example 1: Bridge crane system

Let us consider the bridge crane system used by Moon and VanLandingham [13], where the system is described by four differential equations

```
$$\frac{dx_1}{dt} = x_2$$ (12.15)
```

```
$$\frac{dx_2}{dt} = u$$ (12.16)
```

```
$$\frac{dx_3}{dt} = x_4$$ (12.17)
```

```
$$\frac{dx_4}{dt} = -0.98 x_3 + 0.1 u$$ (12.18)
```

with $\mathbf{x}^T(0) = \mathbf{0}$, and the desired final state is $\mathbf{x}^d = [\ 15\ 0\ 0\ 0\ ]^T$. The constraints on the control are

```
$$-1 \le u \le 1.$$ (12.19)
```

It is required to find the control policy that minimizes the performance index

```
$$I = t_f.$$ (12.20)
```
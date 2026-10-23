```
```cpp
double DiffusionDerivative(double t, double x)
{
    return diffDeriv_(t, x);
}

// Property to set/get initial condition
double InitialCondition() const
{
    return ic_;
}

// Property to set/get time T
double Expiry() const
{
    return exp_;
}
};
```
```

We see that there are two extra data members compared to the SDE class in Chapter 31. Continuing, we note that the corrector step in equation (32.8) takes the averages of the values at the endpoints of the subinterval in question. This is similar to the approach taken by the trapezoid rule (Conte and de Boor, 1981). We now propose a variation of equation (32.8) based on taking values at the midpoint of the subinterval in question (the midpoint rule; Conte and de Boor, 1981):

$X_{n+1}=X_n+\bar{\mu}_{\beta}(\alpha\tilde{X}_{n+1}+(1-\alpha)X_n)\Delta t+\sigma(\beta\tilde{X}_{n+1}+(1-\beta)X_n)\Delta W_n,\quad n\geq 0.\tag{32.10}$

Summarising, schemes (32.8) and (32.10) use corrected drift based on the trapezoid and midpoint rules, respectively. In general, they are more accurate than the Euler method. Furthermore, scheme (32.8) tends to be somewhat more accurate than scheme (32.10), although hard-and-fast rules unfortunately cannot be given. Mathematical and numerical analysis should be supplemented by extensive numerical testing to ensure that a given method is robust and accurate.

We note that equation (32.6) has the same form as equation (32.8), except that we use the drift term rather than the corrected drift term. Likewise, the midpoint equivalent of scheme (32.10) for the case of normal drift is:

$X_{n+1}=X_n+\mu(\alpha\tilde{X}_{n+1}+(1-\alpha)X_n)\Delta t+\sigma(\beta\tilde{X}_{n+1}+(1-\beta)X_n)\Delta W_n,\quad n\geq 0.\tag{32.11}$

We have found schemes (32.6) and (32.11) to be less accurate than schemes (32.8) and (32.10). We now show the code for scheme (32.8), which can be integrated into the software framework (the other schemes are similar in structure):

```
```cpp
class PredictorCorrectorTrapezoidCorrected : public IFdm
{
    // 32.8

private:
    double A;
    double B;
```
```
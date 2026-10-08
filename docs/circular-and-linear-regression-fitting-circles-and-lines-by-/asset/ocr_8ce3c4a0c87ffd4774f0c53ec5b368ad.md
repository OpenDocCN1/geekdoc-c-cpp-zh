# THE CASE OF KNOWN ANGULAR DIFFERENCES

where $\phi_{i}$'s were treated as unknowns, in addition to the circle parameters $(a, b, R)$. Minimization of (4.41) with respect to all its variables was the main idea of the Späth algorithm.

**Berman's model.** In some applications, the differences $\varphi_{i+1}-\varphi_{i}$ between the angular coordinates of successive data points are known. This information can be used to simplify the objective function (4.41), after which the model becomes entirely linear, leading to explicit formulas for parameter estimates.

Indeed, if we denote the known differences by

```
$$\tau_{i} = \varphi_{i} - \varphi_{1} = \sum_{j=1}^{i-1} \varphi_{j+1} - \varphi_{j}$$
```

then we can represent $\varphi_{i} = \varphi + \tau_{i}$, where $\varphi = \varphi_{1}$ is the only unknown angular parameter. Now the objective function (4.41) takes form

```
$$\mathcal{F} = \sum_{i=1}^{n} (x_{i} - a - \alpha \cos \tau_{i} + \beta \sin \tau_{i})^{2} \\
\quad + (y_{i} - b - \alpha \sin \tau_{i} - \beta \cos \tau_{i})^{2}, \quad (4.42)$$
```

where

```
$$\alpha = R \cos \varphi \quad \text{and} \quad \beta = R \sin \varphi \quad (4.43)$$
```

can be treated as auxiliary parameters that (temporarily) replace $R$ and $\varphi$.

Since $\mathcal{F}$ is a quadratic function in its unknowns $a, b, \alpha, \beta$, the model becomes entirely linear. The estimates of $a, b, \alpha, \beta$ can be easily found by setting the partial derivatives of $\mathcal{F}$ to zero and solving the resulting linear system of 4 equations with 4 unknowns. We will not provide details as they are elementary.

Lastly, the radius $R$ (and the base angle $\varphi$, if necessary) can be found from equations (4.43). There is no need for complicated iterative schemes. This model was proposed and solved in 1983 by Berman [15].

**Applications of Berman's model.** Berman [15] pointed out two particular applications where the angular differences are indeed known:

+   1. The calibration of an impedance measuring apparatus in microwave engineering;
2. The analysis of megalithic sites in Britain, in which archaeologists need to fit circles to stone rings.

It is interesting that so much different examples have this important feature in common.

Berman, Griffiths and Somlo [15, 19, 20] present a detailed statistical analysis of the resulting parameter estimates for the model with known angular differences.
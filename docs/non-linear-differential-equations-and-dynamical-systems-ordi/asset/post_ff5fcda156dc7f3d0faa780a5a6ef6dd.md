
## Non-Linear Differential Equations and Dynamical Systems

The differential equation of first order (3.16a) is separable (3.16b):

```
$$\frac{dy}{dx} = \cos x \sqrt{1-y^2}, \quad \int \frac{dy}{\sqrt{1-y^2}} = \int \cos x dx, \quad (3.16a, b)$$
```

and has general integral (3.17a) equivalent to (3.17b):

```
$$\arcsin y = C+\sin x, \quad y(x) = \sin(C+\sin x). \quad (3.17a, b)$$
```

The boundary condition (3.18a) leads to an infinity of values of the arbitrary constant (3.18b):

```
$1=y(0)=\sin C, \quad C=\frac{\pi}{2}+2n\pi.$
```

```
$y(x)=\sin(2n\pi+\frac{\pi}{2}+\sin x)=\sin(\frac{\pi}{2}+\sin x)=\cos(\sin x). \quad (3.18a–c)$
```

all corresponding to the solution (3.18c). Another first-order separable differential equation is considered in the EXAMPLE 10.6.

### 3.2.2 Linear Unforced Differential Equation

If the $g(x, y)$ in the explicit differential equation (3.10a) is linear in the independent variable $y$ and unforced with a coefficient $P(x)$ function of the dependent variable (3.19a):

```
$$\frac{dy}{y}=P(x)y, \quad log y=\int \frac{dy}{y}=\int P(x)dx+\log C, \quad (3.19a, b)$$
```

then the equation is separable (3.11b), and hence solvable by quadratures:

```
$$X(x)=\exp{\{\int P(x)dx\}} \quad y(x)=CX(x). \quad (3.20a, b)$$
```

Thus the linear, unforced (standard LI) first-order differential equation (3.20a) has general integral (3.21a, b). For the example, differential equation (3.22a):

```
$$y'=\left(\frac{1}{x}-x\right)y; \quad y(x)=C\exp(-\frac{x^{2}}{2}+x). \quad (3.21a, b)$$
```

## Differentials and First-Order Equations

has general integral (3.21b)=(3.22b):

```
$P(x)=-\frac{1}{x}; \quad y(x)=C\exp\left(\int^{x} \frac{1}{\xi} d\xi\right)=C\exp\left(\log x-\frac{x^{2}}{2}\right), \quad (3.22a, b)$
```

where in this case was applied (3.20a) with (3.22a). The boundary condition (3.23a) specifies the constant:

```
$1=y(1)=\frac{C}{\sqrt{e}}; \quad y(x)=x\sqrt{e}\exp\left(-\frac{x^{2}}{2}\right)=x\exp\left(\frac{1-x^{2}}{2}\right), \quad (3.23a, b)$
```

in the unique solution (3.23b). Another example of linear unforced differential equation of first order (3.24a) that has general integral (3.24b):

```
$y'=y\tan x; \quad y(x)=C\sec x, \quad (3.24a, b)$
```

as follows from (3.19a) with (3.25a) leading to (3.25b)\equiv$ (3.24b):

```
$P(x)=\tan x; \quad y(x)=C\exp\left(\int^{x} \tan \xi \,d\xi\right)=C\exp\left{-\log(\cos x)\right}=\frac{C}{\cos x}. \quad (3.25a, b)$
```

The boundary condition (3.26a):

```
$1=y(0)=C; \quad y(x)=x\sec x, \quad (3.26a, b)$
```

leads to the unique solution (3.26b):

### 3.3 Linear Forced Differential Equation

The method of variation of parameters (Bernoulli 1697) can be used to obtain a particular integral of the corresponding forced unforced differential equation from the general integral of a linear unforced differential equation with variable coefficients (Notes 1.2–1.4). For example, for: (i) the second-order system with constant coefficients (section 2.9) and (ii) the generalization of (3.19a) as the first-order linear forced differential equation with variable coefficients (standard LII):

```
$y'=P(x)y+Q(x), \quad (3.27)$
```

## Non-Linear Differential Equations and Dynamical Systems

so designated because $y'$ is a linear function of $y$, with coefficients depending on $x$. It will be solved by the method of variation of constants, starting from the solution (3.20a, b) of the unforced equation (3.19a), and replacing the arbitrary constant C by a function C(x) so that the forced equation (3.27) is satisfied. Thus, the solution of the linear forced equation (3.27) is sought in the form:

```
$y(x)=C(x)X(x)=C(x)\exp\left{\int^x P(\xi)d\xi\right};\quad(3.28)$
```

differentiating yields:

```
$y'=(C'+CP)\exp\left{\int^x P(\xi)d\xi\right}=Py+C'X.\quad(3.29)$
```

The equation (3.29) coincides with (3.27), provided that the still-undetermined function C(x) satisfies (3.30a):

```
$Q=C'X,\quad\quad C(x)=C+\int^x\frac{Q(\xi)}{X(\xi)}d\xi,\quad(3.30a, b)$
```

that is, a first-order differential equation whose solution is (3.30b). Substituting (3.30b) in (3.28):

```
$Y(x)=\int^x\frac{Q(\xi)}{X(\xi)}d\xi,\quad\quad y(x)=X(x)[C+Y(x)],\quad\quad(3.31a, b)$
```

it follows that the complete integral (3.31b) of the linear forced (standard LII) first-order differential equation (3.27) consists of: (i) of the general integral (3.20b) of the unforced equation (3.19a), which is the first term on the r.h.s. (3.31b), involving one arbitrary constant beside the function (3.20a); and (ii) the latter also appears in the particular integral of the forced equation (3.27), that is, the second term on the r.h.s. of (3.31b) that involves (3.31a) and no constants of integration. For example the linear forced first-order differential equation (3.32a):

```
$y'=-\frac{y}{x}+\exp(x^2);\quad\quad\quad y(x)=\frac{C}{x}\frac{e^{x^2}}{2},\quad\quad(3.32a, b)$
```

## Differentials and First-Order Equations

has complete integral (3.32b), obtained substituting (3.33a–d)

$P(x)=-\frac{1}{x} \quad X(x)=\exp\left(-\int \frac{d\xi}{\xi}\right)=\exp(-\log x)=\frac{1}{x}, \quad (3.33a, b)

$Q(x)=e^{x^2}: \quad Y(x)=\int \xi e^{\xi^2} d\xi=\frac{1}{2}e^{x^2}, \quad (3.33c, d)

in (3.31b). The boundary condition (3.34a):

$1=y(1)=C+\frac{e}{2}; \quad y(x)=\left(1-\frac{e}{2}\right)\frac{1}{x}\frac{e^{x^2}}{x}-\frac{e^{x^2}}{2x}, \quad (3.34a, b)

leads to the unique solution (3.34b).

Another linear first-order forced first-order differential equation with variable coefficients (3.35a):

$y'=y\cot x+csc x: \quad y(x)=C\sin x-\cos x, \quad (3.35a, b)

whose complete integral is (3.35b), as follows substituting (3.36a–d):

$P(x)=\cot x: \quad X(x)=\exp\left{\int^x \cot \xi d\xi\right}=\\exp[\log(\sin x)]=\sin x \quad (3.36a, b)

$Q(x)=csc x: \quad Y(x)=\int^x csc^2 \xi d\xi=-cot x, \quad (3.36c, d)

in (3.31b). The boundary condition (3.37a):

$1=y\left(\pi/2\right)=C: \quad y(x)=\sin x-\cos x, \quad (3.37a, b)

leads to the unique solution (3.37b). Another linear forced first-order differential equation is considered in the EXAMPLE 10.6.

## Non-Linear Differential Equations and Dynamical Systems

### 3.4 Transformation of Bernoulli (1695)
Non-Linear Differential Equation

The Bernoulli (1695) first-order ordinary differential equation (standard LIII):

```
y' = P(x)y+Q(x)y^n, (3.38)
```

reduces: (i) for n=0 to the linear forced (3.27) standard LII whose integral is (3.20a; 3.31a, b); (ii) for n=1 to the linear forced (0.19a) standard LI with P→Q whose general integral (3.20a, b) is (3.39b):

```
n=1:
y(x)=exp\{\int^x[P(\xi)+Q(\xi)]d\xi\},\n(3.39a, b)
```

In all cases n≠0,1, the Bernoulli (1695) equation (3.38) is a non-linear first-order differential equation (standard LIII) generalizing the linear unforced (standard LIII) Dividing by y^n:

```
n≠1:
Q+Py^{1-n}=y^{-n}'\frac{y^{1-n}'}{1-n},\n(3.40a)
```

it becomes a linear differential equation (3.27), via the transformations:

```
y,P,Q→y^{1-n},(1-n)P,(1-n)Q;
(3.41a–c)
```

the solution (3.31a, b) of (3.40b) is thus (3.31a) [[3.31b]] with the substitutions (3.41b)[3.41a)] leading to (3.42a)[3.42b]:

```
X_n(x)=exp\{\int^xP(\xi)d\xi\},Y_n(x)=(1-n)exp\{\int^x\frac{Q(\xi)}{X_n(\xi)}d\xi\},\n(3.42a, b)
```

where X=X and Y_0=Y. The general integral is analogous to (3.31b):

```
n≠1:
[y(x)]^{-n}=X_n(x)[C+Y(x)],
(3.43a, b)
```

that: (i) coincides with (3.31b) for n=0; (ii) breaks down (3.43a) for n=1, when it is replaced by (3.39a, b). Thus the (standard LIII) Bernoulli (1695) non-linear first-order differential equation (3.38) has solution (Leibniz 1696): (3.39b) in the

## Differentials and First-Order Equations

linear unforced case (3.39a); (3.43a, b) in all non-linear cases $n\neq0,1$, as well as the linear unforced case $n=0$ in (3.31a, b). A simple non-linear case (standard LIV) the particular Riccati equation is (3.44a, b):

```
$n=2: \quad y'=yP(x)+y^2Q(x), \quad y=X_2(x)[C+Y_2(x)], \quad (3.44a-c)$
```

```
$X_2(x)=\exp\left{-\int^x P(\xi)d\xi\right\}, \quad Y_2(x)=-\int^x \frac{Q(\xi)}{X_2(\xi)}d\xi, \quad (3.44d)$
```

whose solution is (3.44c-e). Two examples of the solution of Bernoulli equations are given next, before generalizing (3.44b) to the Riccati equation (sec-3.5).

An example of the non-linear Bernoulli differential equation of particular Riccati type is (3.45a):

```
$xy'==-y+y^2\log x, \quad \frac{1}{y(x)}=Cx+1+\log x, \quad (3.45a, b)$
```

whose complete integral (3.45b) is obtained from (3.44b) with (3.44a–e) using (3.46a–d):

```
$n=2: \quad P(x)=-\frac{1}{x}, \quad X_2(x)=\exp\left(\int^x \frac{d\xi}{\xi}\right)=\exp(\log x)=x \quad (3.46a-d)\nQ(x)=-\frac{\log x}{x}, \quad Y_2(x)=-\int^x \frac{\log \xi}{\xi^2}d\xi=\frac{1+\log x}{x},
```

The last integration (3.46d) can be performed by two methods: (i) integration by parts (3.47):

```
$Y_2(x)=\int^x \frac{\log \xi}{\xi}d\xi=\frac{\log x}{x}-\int^x \frac{1}{\xi}d(\log \xi)=\frac{\log x}{x}-\int^x \frac{d\xi}{\xi^2}=\frac{1+\log x}{x}, \quad (3.47)$
```

or (ii) change of the same variable (3.4a) to obtain the same result (3.48b); (3.47):

```
$$\eta=\frac{1}{\xi};Y_2(x)=-\int^x \log(\frac{1}{\xi})d(\frac{1}{\xi})=-\int_1^{1/x} \log \eta d\eta=-[\frac{\eta}{2} \log \eta - \eta]_1^{1/x}=\frac{1+\log x}{x} \quad (3.48a, b)$$
```

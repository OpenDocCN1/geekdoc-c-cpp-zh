
W — work: 3-9.11
— weight: 4.8.13

## 3 Small Greek Letters

+   $\alpha$ — angle of cylindrical helix: 3.9.5
— coefficient of the cubic term of the quartic potential: 4.5.1
$\beta$ — coefficient of the quartic term in the biquadratic potential: 4.4.4
$\gamma$ — dimensionless non-linearity parameter: 4.4.8
$\omega_0$ — natural frequency: 4.3.2
$\omega_e$ — excitation frequency of parametric resonance: 4.3.2
$\psi$ — non-linearity parameter for a quartic potential: 4.6.1

## 4 Capital Greek Letters

+   $\Phi$ — scalar potential: 3.9.9
— mechanical potential energy: 4.4.2
$\Theta$ — Euler potential: 3.9.9
$\Omega$ — angular velocity of rotation: 4.7.1
$\Psi$ — Euler potential: 3.9.9
$\Xi$ — Clebsch potential: 3.9.9

## 3 Differentials and First-Order Equations

If a differential equation involves derivatives with regard to one (several) variables, it is an ordinary (partial) differential equation; ordinary differential equations it will be considered in the present volume IV, and partial equations in the next volume V. In the dynamics of the second-order linear system with constant (variable) coefficients (chapter 2(4)), the independent variable is time only, leading to an ordinary differential equation. If the particle or system has one (several) degrees of freedom, for example its position is specified by one (system of equations) then the solution of an ordinary differential equation (system of N simultaneous ordinary differential equations), is a function (N functions) of one variable. The derivative of highest order appearing in a differential equation specifies the order of that equation; for example in the differential equation of a particle with one degree of freedom the ordinary differential equation is of order two, because the highest order derivative of position with regard to time is the second, specifying the acceleration. Not all differential equations are readily solvable; this is why it is important to classify them into (i) ordinary or partial, (ii) equations or systems, (iii) one or higher, and (iv) particular standards or sub-types. The aim is to identify classes of differential equations that have certain properties methods of solution. The starting point was the linear differential equations with constant or homogeneous coefficients that have a characteristic polynomial of degree N (chapter 1); analogy other equations with one characteristic polynomial. Considering (i) linear equations with variable coefficients or (ii) non-linear differential equations, it is simpler to solve with those of first order (chapter 3).

After the discussion of general properties of first-order differential equations (section 3.1), methods of solution are presented for eight classes or standards: (i) the separable equation (section 3.2), where the derivative is the ratio of two separate functions of the independent and dependent variable, which can be solved by quadratures; the solution reduces to one (or two) integration(s); (ii) the linear forced equation, a particular case of the separable equation and hence always solvable (section 3.2); (iii) the solution of the linear forced equation is obtained from its forced part by the method of variation of parameters (section 3.3), used before (notes 1.2–1 and section 2.9); (iv) the Bernoulli equation, which is non-linear but can be transformed to the linear type, and hence is always solvable (section 3.4); (v) the Riccati equation, while there is no known general solution,

## Non-Linear Differential Equations and Dynamical Systems

a non-linear generalization of the Bernoulli equation (section 3.6), and it can be shown (section 3.5) if one/two/three particular integrals are known, then the general integral can be obtained via two/one quadratures.

A sixth method is (vi) a change of variable that may render a differential equation solvable; for the homogeneous first-order differential equation, in which the dependent and independent variable appear only through their ratio, can be transformed into a separable variable, and hence integrated in all cases (section 3.7). Proceeding from the first to the next two classes, any first-order differential equation is equivalent to a first-order in two variables (section 3.8) leading to two cases: (vii) if it satisfies a condition of integrability, it is an exact differential that is of a function, equated to an arbitrary constant the general integral; (viii) if the integrability condition is not satisfied, the first-order differential equation is equivalent to an inexact differential, and is not the differential of a function, though it becomes when multiplied by an integrating factor that always exists. This is no longer the case for a first-order differential in three variables (section 3.9), when there are three possibilities: (i/ii) exact (inexact) satisfying (not satisfying) an integrability condition and not needing (needing) an integration factor, as for a first-order differential in two variables; (ii/iii) the existence (non-existence) of an integrating factor depends on the satisfaction (non-satisfaction) of a more general integrability condition. The first-order differential may be extended to: (i) more than three variables (notes 3.11–3.15); (ii) homogeneous differentials (notes 3.16–3.20); (iii) higher-order differentials (notes 3.21–3.24).

### 3.1 General Properties of First-Order Equations

The general properties include a classification of solutions (subsection 3.1.1) and the determination of the arbitrary constant in the general integral (subsection 3.1.2). The differential equation is considered to be solved when it is reduced to an integration (subsection 3.1.3) or quadrature (subsection 3.1.4) that may be elementary or not. The general integral of a first-order differential equation is one family (or several families) of integral curves [subsection 3.1.1 (3.5)], and each value of the arbitrary constant corresponds to one of the curve (of each family).

### 3.1.1 General Integral and Integral Curves

An ordinary differential equation of the first order is a relation between a function y(x), its variable x, and its first derivative y':

```
y' = \frac{dy}{dx}; \quad F(x,y;y') = 0. \quad (3.1a, b)
```

## Differentials and First-Order Equations

![](img/6a4cb3b3bd1429197bb791c4b642651c_25_0.png)

FIGURE 3.1
An explicit first-order differential equation specifies one slope at each point of the plane and its solution is an integral curve with the corresponding tangents.

The function y(x) is the dependent variable, and the variable x is the independent variable. A solution of the differential equation is a function y(x) that satisfies it (3.1b) when substituted together with its first derivative (3.1a). The solution of the differential equation (3.1a, b) may be given a geometric interpretation (Figure 3.1); the first-order ordinary differential (3.1b) specifies at each point of the (x, y)-plane one (or more) slopes y'. A solution must be a curve, whose tangent at the point (x, y) has a slope y' and is called an integral curve. Since it specifies one (or more) slopes or tangents at each point, the most general solution is a family of curves (Figure 3.2):

```
$f(x, y, C) = 0 \quad\quad (3.2)$
```

involving a parameter C, and this is the general integral of the first order ordinary differential equation (3.1b). Giving to the parameter C as a particular value C=Cv specifies a particular curve, or a particular integral of the differential equation. Thus an ordinary differential of first order relates a family of curves (3.2) to the slopes (3.1a) of its tangents at each point (x, y). The cases in which the tangent is not unique may lead to more than one family of integral curves or to curves with multiple points, the simplest being double points (Figure 3.3). If the family of integral curves has an envelope this a singular or special integral (section 1.1); the locus of double points or other loci may also lead to special integrals (sections 5.1–5.4).

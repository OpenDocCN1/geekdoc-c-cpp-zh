
solution; and (iii) the sum of discretization, systematic, and truncation errors does not call into question the accuracy of the results. It may be that the steps (i) to (iii) are harder than the application of the numerical method “ad hoc”; the later approach may lead to overflows or underflows, numerical “instabilities”, dispersion of results, non-convergence, or simply to an apparently neat convergence that there is no guarantee of correctness of the final result. If the final result is correct there may still be the choice of interpretation of its meaning, that may be helped by some of the earlier approaches.

## NOTE 4.6: Complementarity of the Four Methods of Solution

The preceding account on qualitative (note 4.2) and quantitative analytical exact (note 4.3) [approximate (note 4.4)] and numerical (note 4.5) methods of differential equations shows each has strengths and weaknesses, and the best approach is to combine all four methods to use the strengths of some to overcome the weaknesses of the others. Starting with a differential equation (A) can establish: (A.1) the existence of solution; (A.2) the boundary/or initial conditions for the unity of solution; (A.3) the stability conditions; and (A.4) the singularities or bifurcations and associated properties. The next differential equation is restricted to form a amenable to analytical solution (B): (B.1) the qualitative theory (A) indicates (B.2) the method chosen must specify the solution completely; (B.3) any issues of validity, like convergence of an infinite representation, need to be settled; and (B.4) the interpretation of the solution should lead to a good understanding of the phenomena and processes it describes.

The exact analytical solution (B) may be more restricted in its domain of application, so is still amenable to approximate analytical solution (C): (C.1) the approximation(s) must be carefully chosen not to exclude some of the essential aspects being investigated; (C.2) once the approximation(s) is(are) the solution should be exact, without any simplifications except that are a consequence of previous approximations; (C.3) the results should be interpreted, in mind that some properties may not be general and are a byproduct-of the approximations made at the beginning; (C.4) it should be borne in mind that other solutions and properties may have been excluded by the approximations. The “real” problem due to a complex geometry, or/and inhomogeneous media, complex forcings, may not be amenable to exact (B) or approximate (C) analytical solution without excessive “idealization”, so a numerical solution (D) is sought: (D.1) the numerical method should be chosen so to converge to the unique solution specified by the qualitative theory (A); (D.2) the presence of singularities or bifurcations may require separate treatment to avoid numerical instabilities or wrong matches across a special points; (D.3) the discretization, systematic, and truncation errors should be consistent with the required accuracy; and (D.4) the results should be interpreted with as much insight as could be gained from the preceding approaches (A, B, C).

## NOTE 4.7: Comparison of Methods in a Sample Case

The thorough $4 \times 4 = 16$ step approach (note 4.6) to the solution of a differential equation is not always or often applied. In the cases of some standard differential equations, e.g., linear with constant coefficients, the general properties are already well-known; in the case of non-linear differential equations and/or variable coefficients, starting a numerical algorithm while ignoring singularities/or bifurcations could: (i) lead to instabilities or overflows, signaling that something is amiss; (ii) lead to a wrong result, without any warning; or (iii) lead to the right result if the method fortuitously matched the properties of the solution. Next is considered the numerical solution of a rather simple differential equation so that the exact analytical and approximate numerical approaches can be compared in detail. As a numerical method this is the simplest of samples.

## NOTE 4.8: Definition and Discretization of Derivatives of Any Order

The first-order **derivative** is defined as the slope (Figure 4.35a) or limit of the incremental ratio as the **step size** tends to:

$$f'(x) = \lim_{h\to 0} \frac{f(x+h) - f(x)}{h}, \quad (4.511)$$

if it exists. It follows that the second-order derivative (Figure 4.35b) is given by:

$$f''(x) = \lim_{h\to 0} \frac{f'(x+h) - f'(x)}{h} = \lim_{h\to 0} \frac{f(x+2h) - 2f(x+h) + f(x)}{h^2}. \quad (4.512a, b)$$

Applying the definition of derivative (4.511) it inevitably follows that the derivative of order n is given by:

$$f^{(n)}(x) = \lim_{h\to 0} h^{-n} \sum_{k=0}^{n} (-1)^{n-k} \binom{n}{k} f(x + kh). \quad (4.513)$$

The proof of (4.513) is made by induction: (i) it holds for $n=1(n=2)$ when it reduces to (4.511) ([4.512b]); (ii) if it holds for $n$ it also holds for $n+1$. The proof of item (ii) follows starting from the definition of derivative (4.511) applied to $f^{(n)}(x)$:

$$f^{(n+1)}(x) \equiv \lim_{h\to 0} \frac{f^{(n)}(x+h) - f^{(n)}(x)}{h} \quad (4.514a)$$

## Unsteady, Non-Linear, and Chaotic Systems

![](img/6a4cb3b3bd1429197bb791c4b642651c_278_0.png)

![](img/6a4cb3b3bd1429197bb791c4b642651c_278_1.png)

FIGURE 4.35
The numerical solution of a differential equation is based on the discretization of the derivatives leading to a finite difference equation. The first-order derivative or tangent is replaced by a secant (a), the second-order derivative or curvature is replaced by a secant of secants (b), and so on for higher orders.

Substitution of (4.513) that is assumed to hold leads to:

$$f^{(n+1)}(x) = \lim_{h\to 0} h^{-1} \left[ f^{(n)}(x+h)-f^{(n)}(x) \right]$$
$$= \lim_{h\to 0} h^{-1-n} \sum_{k=0}^{n} (-1)^{n-k} \binom{n}{k} f(x + kh)$$

## Unsteady, Non-Linear, and Chaotic Systems (Wait, the prompt text repeats the headers "Unsteady, Non-Linear, and Chaotic Systems" twice in the OCR. I will maintain the structure as provided in the OCR but cleaned of artifacts.)

*(Self-correction: The OCR text has the header "Unsteady, Non-Linear, and Chaotic Systems" appearing twice. I will treat them as section headers as in the document flow.)*

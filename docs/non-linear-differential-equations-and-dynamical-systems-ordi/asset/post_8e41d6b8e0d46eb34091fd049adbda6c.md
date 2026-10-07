
# Non-Linear Differential Equations and Dynamical Systems

In this case the general integral is (3.284c), involving a twice continuously differentiable function (3.277a) that specifies a family of hypersurfaces orthogonal to the vector field (3.283a).

### NOTE 3.5: Integrable Differential in N Variables

As an example, consider the first-order differential in four variables (3.285):

$$0 = x_2 dx_1 + x_1 dx_2 + \frac{x_1x_2}{x_4} dx_3 - \frac{x_1x_2x_3}{(x_4)^2} dx_4, \quad (3.285)$$

with vector coefficients (3.286a) that has (3.278c) non-zero curl (3.286b):

$$X_m = \{x_2, x_1, \frac{x_1x_2}{x_4} - \frac{x_1x_2x_3}{(x_4)^2} \};$$

$$\{\Omega_{12}, \Omega_{13}, \Omega_{14}, \Omega_{23}, \Omega_{24}, \Omega_{34}\} = \{0, \frac{x_2}{x_4}, - \frac{x_2x_3}{(x_4)^2}, \frac{x_1}{x_4}, - \frac{x_1x_2x_3}{(x_4)^3} \}, \quad (3.286a, b)$$

Since the curl (3.274b) is a bivector, that is, skew-symmetric $4 \times 4$ matrix, it has six independent components (3.286b); the curl (3.286b) is not zero, proving that the differential (3.285) is inexact. The integrability conditions are skew-symmetric in three indices (m, n, s) = (1,2,3,4) taking values, there are four independent components, for each “missing” index in the helicity:

$$\Omega_{12}X_4 + \Omega_{23}X_1 + \Omega_{31}X_2 = 0 = \Omega_{12}X_4 + \Omega_{24}X_1 + \Omega_{41}X_2,$$
$$\Omega_{13}X_4 + \Omega_{34}X_1 + \Omega_{43}X_3 = 0 = \Omega_{23}X_4 + \Omega_{34}X_2; \quad (3.287a–d)$$

since all integrability conditions (3.287a–d) are met, the differential (3.285) has an integrating factor. The integrating factor may be found noting that (i) the first two terms of the differential (3.285) are exact (3.288a):

$$x_2 dx_1 + x_1 dx_2 = d(x_1x_2); \quad \frac{x_1x_2}{x_4} - \frac{x_1x_2x_3}{(x_4)^2} dx_4 = x_1x_2d(\frac{x_3}{x_4}) \quad (3.288a, b)$$

(ii) the last two terms (3.288b) of the differential (3.285) becomes exact multiplying by (3.289a); and (iii) although the first two terms (3.288a) are exact, they remain when multiplied by (3.289a). Thus (3.289a) is an integrating factor for the complete differential in four variables (3.285) as follows from (3.289b):

$$\lambda = \frac{1}{x_1x_2} : x_2dx_3 + x_1dx_2 + (x_1x_2/x_4)dx_3 - [x_1x_2x_3/(x_4)^2]dx_4$$
$$x_1x_2 \frac{dx_1}{x_1} + \frac{dx_2}{x_2} + \frac{dx_3}{x_4}(x_4)^2 = d \left[\log(x_1x_2) + \frac{x_3}{x_4}\right] \quad (3.289a, b)$$

the exact differential (3.289b) specifies the general integral:

$$x_1x_2 \exp \frac{x_3}{x_4} = C. \quad (3.290)$$

Thus the first-order differential in four variables (3.285) with vector of coefficients (3_286a) is inexact (3.286b) but (3.287a–d) an integrating factor (3.289a) leading to the general integral (3.290); the latter specifies a family of hypersurfaces in the four-dimensional space orthogonal to the vector field (3.286a).

# NOTE 36: Curves on a Surface Orthogonal to a Vector Field

If the first-order differential in N variables (3.274a, b) with continuously differentiable vector field of coefficients (3.283a) does not meet the Beltrami conditions of zero helicity (3.282), then it is inexact; that is, it has non-zero curl (3.291c) and has no integrating factor:

$$X_n \in C^1(R^N): \quad X_n dx_n = 0, \quad \Omega_{mn} = \partial_m x_n - \partial_n x_m \neq 0 = \sum_{m,n} X_m\Omega_{mn} \quad (3.291a–d)$$

this leads to the Pfaff problem: (3.292) independent conditions (3.292b) can be imposed:

$$r=1,...,N-2: \quad \Psi_r(x_1,...,x_n)=0, \quad \left(\frac{\Psi_r}{\partial x_n}\right)=N-2, \quad (3.292a–c)$$

where the functions (3.293b) are continuously differentiable (3.293a):

$$\Psi_r \in C^1(R^N): \quad 0=d\Psi_r = \sum_{\eta=1}^N \frac{\Psi_r}{\partial x_\eta}dx_\eta \quad (3.293a, b)$$

# 68 Non-Linear Differential Equations and Dynamical Systems

From (3.292c) it follows that (3.293b) can be solved (3.294a–c) for the differentials $dx_3, \dots dx_N$ in terms of $(dx_1, dx_2)$:

$$n=1,...,N; \quad s=3,...,N; \quad dx_s = A_s dx_1 + B_s dx_2 \quad (3.294a-c)$$

Substitution of (3.294c) leads to a differential in two variables (3.295a, b):

$$0 = \sum_{n=1}^{N} X_n dx_n = \sum_{n=1}^{3} X_n dx_n + (X_2 + \sum_{n=3}^{N} B_n) dx_2 = Y_1 dx_1 + Y_2 dx_2. \quad (3.295a, b)$$

The latter (3.295b) has an integrating factor (3.296a) leading to the general integral (3.296b):

$$\lambda(Y_1 dx_1 + Y_2 dx_2) = d\Phi, \quad \Phi(x_n) = C. \quad (3.296a, b)$$

The geometric interpretation is: (i) the N-2 (3.293a) hypersurfaces (3.292a, b) intersect (3.292c) in a surface or subspace of dimension $M=2$; and (ii) on this surface there are curves, namely the intersection with the general integral (3.296b), that are orthogonal to the vector field (3.291a) of coefficients.

# NOTE 3.7: Inexact Differential in Four Variables without Integrating Factor

The first-order differential in four variables:

$$0 = x_2 dx_1 + x_1 dx_2 + x_4 dx_3 - x_3 dx_4, \quad (3.297)$$

has no integrating factor, because: (i) first two terms are an exact differential (3.298):

$$x_2 dx_1 + x_1 dx_2 = d(x_1 x_2); \quad (3.298)$$

(ii) the last two terms (3.299b) have an integrating factor (3.299a):

$$\lambda = \frac{1}{X_3 X_4} \quad \frac{x_4 dx_3 - x_3 dx_4}{x_3 x_4} = d \left[ \log \left(\frac{x_3}{x_4}\right) \right], \quad (3.299a, b)$$

and (iii) there is no common integrating factor the exact differential (3.297) multiplied by (3.299a) becomes inexact. It can be checked that the vector of coefficients (3.300a):

$$\bar{X} = \{x_2, x_1, x_4, -x_3\}: \quad \{\Omega_{12}, \Omega_{13}, \Omega_{14}, \Omega_{23}, \Omega_{24}, \Omega_{34}\} = \{0, 0, 0, 0, 0, -2\}, \quad (3.300a, b)$$

# Differentials and First-Order Equations

has curl (3.300b) with one non-zero component, arising from the last two terms in (3.297). The Beltrami conditions (3.282) are not met because of the same term; that is, (3.287a, b) hold not (3.287c, d), that are integrating by:

$$\Omega_{23}X_4 + \Omega_{34}X_2 + \Omega_{41}X_3 = -2X_2, \quad \Omega_{23}X_4 + \Omega_{34}X_2 + \Omega_{42}X_3 = -2X_i \quad (3.301a, b)$$

$$0 = \Psi_1(x_1, x_2, x_3) = x_3 - x_2, \quad 0 = \Psi_2(x_1, x_2, x_4) = x_4 - x_1 + x_2 \quad (3.302a, b)$$

reduces the differential from (3.297) to three variables:

$$0 = x_2 dx_1 + x_1 dx_2 + (x_1 - x_2)d(x_1 + x_2) - (x_1 + x_2)d(x_1 - x_2) = -x_2 dx_1 + 3x_1 dx_2 \quad (3.303)$$

the differential equation (3.303) is separable (3.304a):

$$0 = 3 \frac{dx_2}{x_2} - \frac{dx_1}{x_1} = d(3\log x_2 - \log x_1), \quad x_1 = C(x_2)^3, \quad (3.304a, b)$$

leading to the integral (3.304b). Thus the first-order differential in four variables (3.297) is inexact (3.300b) and has no integrating factor (3.301a, b); imposing two conditions (3.302a, b) the general integral is (3.304b). Thus the family of curves (3.304b) on the surface that is the intersection of the two hypersurfaces (3.302a, b), is orthogonal to the vector field (3.300a).

# NOTE 8: Independent Components of the Curl and Helicity

Given a first-order differential (3.276a, b) in N variables associated with the vector of coefficients (3.283a) may be considered: (i) the **curl** (3.283b); that is, a skew-symmetric tensor or bivector, with $N^2$ components (3.305a) of which are independent (3.305b), as diagonal of $N \times N$ matrix:

$$\Omega_{mn} = N^2, \quad \Omega_{mn} = \frac{N^2}{2} - \frac{N}{2} \frac{N(N-1)}{2} \begin{pmatrix} N \end{pmatrix} \quad (3.305a, b)$$

(ii) the *helicity* (3.282); that is, a covariant skew-symmetric tensor with three indices or trivector that has (3.306a) components of (3.306b) are independent:

$$H_{mnis} = N^3, \quad H'_{mnis} = \frac{N(N-1)(N-2)}{6}. \quad (3.306a, b)$$

In cases of the bivector (3.305a, b): [trivector (3.306a, b)]: repeated indices lead to zero by skew-symmetry; and the same set of indices in any order gives the same values with minus sign for even (odd) permutations. For a bivector (3.305a) the first index takes N values, the second index takes N-1 values, and the product is divided by permutations of 2, leading to (3.305b). For a trivector (3.306a) the third index takes N-2 values and the product is divided by permutations of 3! leading to (3.306b). An N-dimensional differentiable vector field has a curl vector (3.291c) [Helicity trivector (3.291d)] with (3.305a) (3.306b) components of which (3.305b) [3.306b] are independent, and are indicated in the Table 3 for N=1,...,10 together with the number of hypersurfaces (3.292a, b) with linearly independent normal vectors (3.292c) that appear in the Pfaffian (standard LXXXIV).

# TABLE 3.2
Number of Independent Components of the Curl and Helicity

| Space | Field | Curl | Helicity | Constraints |
| :--- | :--- | :--- | :--- | :--- |
| Coordinates | Vector | Bivector | Trivector | Hypersurfaces |
| X_m | X_m | $\Omega_{mn} = \partial_m x_n - \partial_n x_m$ | $H_{mnr} = \sum_{r} X_r(\partial_m x_n - \partial_n x_m)$ | $\Psi_l(X_n) = 0$ |
| N | N | N(N-1)/2 | N(N-1)(N-2)/6 | N-2 |
| N-1 | 1 | 0 | 0 | - |
| N-2 | 1 | 1 | 0 | - |
| N-3 | 3 | 3 | 1 | 1 |
| N-4 | 4 | 6 | 4 | 2 |
| N-5 | 5 | 10 | 10 | 3 |
| N-6 | 6 | 15 | 20 | 4 |
| N-7 | 7 | 21 | 35 | 5 |
| N-8 | 8 | 28 | 56 | 6 |
| N-9 | 9 | 36 | 84 | 7 |
| N-10 | 10 | 45 | 120 | 8 |

Note: Total number of components and number of independent components of the bivector curl and trivector field of a vector field in N dimensions.


## References

[1] M. J. Ablowitz, A. S. Fokas, and Z. H. Musslimani, *On a new non-local formulation of water waves*, J. Fluid Mech. **562** (2006), 313–343, DOI 10.1017/S0022112006001091. MR2263547 (2007k:76013)

[2] M. J. Ablowitz and T. S. Haut, *Spectral formulation of the two fluid Euler equations with a free interface and long wave reductions*, Anal. Appl. (Singap.) **6** (2008), no. 4, 323–348, DOI 10.1142/S0219530508001213. MR2459114 (2010a:76016)

[3] C. T. Bishop and M. A. Donelan. Measuring waves with pressure transducers. *Coastal Engineering*, 11:309–328, 1987.

[4] D. Clamond and A. Constantin, *Recovery of steady periodic wave profiles from pressure measurements at the bed*, J. Fluid Mech. **714** (2013), 463–475, DOI 10.1017/jfm.2012.490. MR3008068

[5] R. R. Coifman and Yves Meyer, *Nonlinear harmonic analysis and analytic dependence*, Pseudodifferential operators and applications (Notre Dame, Ind., 1984), Proc. Sympos. Pure Math. vol. 43, Amer. Math. Soc., Providence, RI, 1985, pp. 71–78, DOI 10.1090/pspum/043/812284. MR812284

[6] A. Constantin, *On the recovery of solitary wave profiles from pressure measurements*, J. Fluid Mech. **699** (2012), 376–384, DOI 10.1017/jfm.2012.114. MR2923684

[7] Adrian Constantin, Joachim Escher, and Hung-Chu Hsu, *Pressure beneath a solitary water wave: mathematical theory and experiments*, Arch. Ration. Mech. Anal. **201** (2011), no. 1, 251–269, DOI 10.1007/s00205-011-0396-0. MR2807138 (2012f:76032)

[8] Walter Craig and David P. Nicholls, *Travelling two and three dimensional capillary gravity water waves*, SIAM J. Math. Anal. **32** (2000), no. 2, 323–359, DOI 10.1137/S0036141099354181. MR1781220 (2002c:76016)

[9] W. Craig and C. Sulem, Numerical simulation of gravity waves, J. Comput. Phys. **108** (1993), no. 1, 73–83, DOI 10.1006/jcph.1993.1164. MR1239970 (94h:76064)

[10] Bernard Deconinck and Katie Oliveras, *The instability of periodic surface gravity waves*, J. Fluid Mech. **675** (2011), 141–167, DOI 10.1017/S0022112011000073. MR2801039 (2012j:76057)

[11] B. Deconinck, K. L. Oliveras, and V. Vasan, *Relating the bottom pressure and the surface elevation in the water wave problem*, J. Nonlinear Math. Phys. **19** (2012), no. suppl. 1, 1240014, 11, DOI 10.1142/S14029251124000141. MR2999408

[12] T. Levi-Civita, *Détermination rigoureuse des ondes permanentes d’amplitude finie* (French), Math. Ann. **93** (1925), no. 1, 264–314, DOI 10.1007/BF01449965. MR1512238

[13] Katie Oliveras and Vishal Vasan, *A new equation describing travelling water waves*, J. Fluid Mech. **717** (2013), 514–522, DOI 10.1017/jfm.2012.591. MR3018618

[14] K. L. Oliveras, V. Vasan, B. Deconinck, and D. Henderson, *Recovering the water-wave profile from pressure measurements*, SIAM J. Appl. Math. **72** (2012), no. 3, 897–918, DOI 10.1137/110853285. MR2968755

[15] Pavel I. Plotnikov and John F. Toland, *The Fourier coefficients of Stokes’ waves*, Nonlinear problems in mathematical physics and related topics, I, Int. Math. Ser. (N. Y.) vol. 1, Kluwer/Plenum, New York, 2002, pp. 303–315, DOI 10.1007/978-1-4615-0777-2.18. MR1970618 (2004c:76023)

[16] D. J. Struik, *Détermination rigoureuse des ondes irrotationnelles périodiques dans un canal à profondeur finie* (French), Math. Ann. **95** (1926), no. 1, 595–634, DOI 10.1007/BF01206629. MR1512296

[17] J. F. Toland, *Stokes waves*, Topol. Methods Nonlinear Anal. **7** (1996), no. 1, 1–48. MR1422004 (97j:35130)

[18] Vishal Vasan and Bernard Deconinck, *The Bernoulli boundary condition for traveling water waves*, Appl. Math. Lett. **26** (2013), no. 4, 515–519, DOI 10.1016/j.aml.2012.12.008. MR3019985

[19] Vishal Vasan and Bernard Deconinck, *The inverse water wave problem of bathymetry detection*, J. Fluid Mech. **714** (2013), 562–590, DOI 10.1017/jfm.2012.497. MR3008073

[20] V. Vasan and K. L. Oliveras. Pressure beneath a traveling wave with constant vorticity. *submitted for publication*, 2013.

Mathematics Department, Seattle University, Seattle, Washington 98102
*E-mail address:* `oliveras@seattleu.edu`

Department of Mathematics, Pennsylvania State University, University Park, Pennsylvania 16802
*E-mail address:* `vasan@math.psu.edu`

## Comparison of Five Methods of Computing the Dirichlet–Neumann Operator for the Water Wave Problem

Jon Wilkening and Vishal Vasan

ABSTRACT. We compare the effectiveness of solving Dirichlet–Neumann problems via the Craig–Sulem (CS) expansion, the Ablowitz–Fokas–Musslimani (AFM) implicit formulation, the dual AFM formulation (AFM*), a boundary integral collocation method (BIM), and the transformed field expansion (TFE) method. The first three methods involve highly ill-conditioned intermediate calculations that we show can be overcome using multiple-precision arithmetic. The latter two methods avoid catastrophic cancellation of digits in intermediate results, and are much better suited to numerical computation.

For the Craig–Sulem expansion, we explore the cancellation of terms at each order (up to 150th) for three types of wave profiles, namely band-limited, real-analytic, or smooth. For the AFM and AFM* methods, we present an example in which representing the Dirichlet or Neumann data as a series using the AFM basis functions is impossible, causing the methods to fail. The example involves band-limited wave profiles of arbitrarily small amplitude, with analytic Dirichlet data. We then show how to regularize the AFM and AFM* methods by over-sampling the basis functions and using the singular value decomposition or QR-factorization to orthogonalize them. Two additional examples are used to compare all five methods in the context of water waves, namely a large-amplitude standing wave in deep water, and a pair of interacting traveling waves in finite depth.

## 1. Introduction

The water wave equations, also known as Euler’s equations for inviscid, irrotational waves, describe the motion of the free surface of an ideal fluid. For periodic waves in two dimensions over a flat surface in the absence of surface tension, they are given as follows [9]:

```
φ_xx + φ_yy = 0,      −h < y < η,
η_t + φ_x η_x = φ_y,    y = η(x,t),
φ_t + 1/2 φ_x² + 1/2 φ_y² + g η = 0,    y = η(x,t),
φ_y = 0,               y = −h.
```

Here φ is the velocity potential (related to the fluid velocity by u = ∇φ), η is the graph of the free surface of the water, g is the acceleration of gravity, h is the

depth of the undisturbed fluid, and subscripts denote partial derivatives. Since we are interested in periodic waves, we consider periodic boundary conditions in the horizontal direction. We note that the above equations represent a free-boundary value problem for Laplace’s equation, i.e. both η and φ are unknowns. These equations readily generalize to three-dimensional fluids (with two-dimensional surfaces); however, in the present work, we limit ourselves to one-dimensional surfaces.

The water-wave equations may be reformulated in terms of only the surface variables η(x, t) and q = φ(x, η, t) as [11,33]

```
∂η/∂t = G(η)q,
∂q/∂t = -gη - q_x²/2 + (G(η)q + η_x q_x)² / [2(1 + η_x²)],
```

where G(η) represents the Dirichlet-Neumann operator (DNO) defined as

```
G(η)q = φ_y(x, η) - η_x φ_x(x, η),
```

where φ is the solution to the following boundary-value problem

```
φ_xx + φ_yy = 0,      -h < y < η,
φ(x, y) = q(x),      y = η,
φ_y = 0,             y = -h.
```

Thus G(η) maps the given Dirichlet data q to the associated Neumann data at the free surface. Consequently, to evolve the surface variables in time using some numerical scheme, we require the solution to Laplace’s equation at every time step. Numerically solving Laplace’s equation at every time step is expensive, particularly in three dimensions.

A characterization of G(η) that avoids the expensive numerical solution of Laplace’s equation is appealing. In the current work we discuss four such characterizations developed in the context of water waves. These four methods are the operator expansion method of Craig & Sulem (CS) [11], the transformed field expansion method (TFE) of Bruno & Reitich [7] and Nicholls & Reitich [23,24], the nonlocal implicit formulation of the DNO given by Ablowitz, Fokas & Musslimani (AFM) [1], and a dual version to the AFM method, derived by Ablowitz & Hal [2], which we denote by AFM*. Each of these methods has had remarkable theoretical utility in deriving reduced models for water waves in various physical regimes [10], in deriving conserved quantities [1], and also in providing the theoretical framework to pose some inverse problems [25,28]. Additionally, each of these methods readily generalizes to the case of both varying bottom boundaries and three dimensional fluids.

Of course, many traditional methods to numerically solve Laplace’s equation exist, including the boundary integral method, conformal mapping techniques, and the finite element method. In the present work we chose to compare the CS and TFE operator expansions and the AFM/AFM* nonlocal formulations with the boundary integral method. We do not consider conformal mapping [14], as it does not extend to three dimensional problems, nor traditional finite elements [26], as the trade-off between high-order elements and sparsity of the stiffness matrix makes them expensive when high accuracy is desired. Though it is not usually described in this way, we regard the TFE method as a spectrally accurate variant of the finite element method. The boundary integral method is particularly efficient in two
dimensions.

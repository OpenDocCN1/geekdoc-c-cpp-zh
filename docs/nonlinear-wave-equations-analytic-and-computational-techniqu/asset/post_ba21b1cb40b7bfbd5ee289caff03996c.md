
With the purpose of bringing together researchers working on these different problems, a special session called “Nonlinear Waves and Integrable Systems” was organized at the AMS Western Sectional Meeting in Boulder, Colorado, in the spring of 2013. The organizers were fortunate in having such a diverse group of speakers agree to present their research and commit to write a research paper for this volume which attempts to capture the scope of the special session. While by no means exhaustive, this volume addresses and explains many of the major analytic and computational techniques used across several sub-disciplines of the study of nonlinear wave equations.

The volume begins with an article by Ben Herbst, Garrett Nieddu, and A. David Trubatch who return to questions from the genesis of the field of integrable systems. The authors study whether discretizations of continuous integrable systems inherit their dynamic properties, in this case “recurrence,” from the integrability of the continuous model.

Next, a series of papers on techniques related to the IST is presented. Francesco Demontis, Cornelis van der Mee, and Federica Vitale study the scattering data of a defocusing Zakharov–Shabat system with non-zero boundary conditions. This problem is of particular relevance to the study of dispersive shock-waves, a subject of much recent interest.

The next two papers address questions related to the Novikov–Veselov (NV) equation, a two-dimensional generalization of the KdV equation. The first paper, co-authored by Ryan Croke, Jennifer L. Mueller, Michael Music, Peter Perry, Samuli Siltanen, and Andreas Stahel, is devoted to the use of the IST to study the NV equation. The authors illustrate the use of powerful techniques from inverse problems and scattering theory to determine for what types of initial conditions the NV equation is well-posed. In the second paper, the stability of particular solutions to the NV equation is studied by Ryan Croke, Jennifer L. Mueller, and Andreas Stahel.

One last paper concerned with integrable systems is written by Gregory Lyng who studies the semi-classical limit of the focusing NLS equation showing the role of Riemann–Hilbert problems in investigating integrable systems.

The subsequent series of papers addresses questions on the free surface problem in fluids. The first paper by Jon Wilkening looks at a classic question on the correspondence of phenomena found in the KdV equation and the free surface problem from which the KdV equation is derived.

In the next paper, Katie Oliveras and Bernard Deconinck investigate modulational instabilities in the free surface problem. Modulational instabilities were first found in the NLS equation, which is derived from the free surface problem. Using a formulation of the free surface problem first proposed by Ablowitz, Fokas and Musslimani (AFM) – an approach strongly motivated by methods from integrable systems – the authors extend the results from the NLS equation to a more physically realistic model.

In the same spirit, Katie Oliveras and Vishal Vasan show how to use the AFM formulation to determine the height of free surface waves from pressure measurements along the “sea-floor”. This work has practical importance for oceanographers, and represents a significant improvement over existing methodologies.

Finally, Jon Wilkening and Vishal Vasan investigate several competing numerical schemes for simulating the free surface problem. The merits and drawbacks of the AFM approach for numerical solutions are examined in detail, and superior alternatives to this approach are provided and explained.

The editors wish to thank the authors who contributed to this volume. Without their diligent efforts this volume would not exist. Likewise, we wish to express our gratitude to the anonymous reviewers who helped to make this volume a strong contribution to the nonlinear waves and broader mathematical community. Finally, we would like to thank all of the participants in the special session who helped to motivate the creation of this volume.

Christopher W. Curtis
Anton Dzhamay
Willy A. Hereman
Barbara Prinari

## List of Special Session Participants

- Douglas E. Baldwin, University of Colorado Boulder
- Michael Benfield, North Carolina State University
- Gino Biondini, State University of New York at Buffalo
- Sarbarish Chakravarty, University of Colorado Colorado Springs
- Christopher W. Curtis, University of Colorado Boulder
- Francesco Demontis, Università di Cagliari
- Anton Dzhamay, University of Northern Colorado
- Willy A. Hereman, Colorado School of Mines
- Mark A. Hoefer, North Carolina State University
- Matthew Johnson, University of Kansas
- Stéphane Lafortune, College of Charleston
- Héctor E. Lomelí, University of Texas at Austin
- Gregory Lyng, University of Wyoming
- Kenichi Maruno, University of Texas Pan-American
- Jennifer L. Mueller, Colorado State University
- Katie Oliveras, Seattle University
- Peter A. Perry, University of Kentucky
- Barbara Prinari, University of Colorado Colorado Springs
- Harvey Segur, University of Colorado Boulder
- Thomas Trogdon, University of Washington
- Vishal Vasan, Pennsylvania State University
- Jon Wilkening, University of California, Berkeley

## Recurrence in the Korteweg–de Vries equation?

Ben Herbst, Garrett Nieddu, and A. David Trubatch

ABSTRACT. The Zabusky–Kruskal lattice (ZK) was derived as a finite-difference approximation of the Korteweg–de Vries equation for the purpose of numerical simulation of that PDE. Like the Fermi–Pasta–Ulam lattice from which it was ultimately derived, ZK was also observed to exhibit near-recurrence of its initial state at regular time intervals. The recurrence has not been completely explained, though it has been attributed to the solitons or, less specifically, the integrability of the KdV continuum limit. The attribution of recurrence to the integrability of the continuum limit (i.e., KdV) leads naturally to the hypotheses that simulations (i) on smaller grid separations, (ii) with discretizations that are integrable as spatially discrete systems or (iii) with higher-order discretizations should all exhibit stronger recurrences than observed in the original simulations of ZK. However, systematic simulations over a range of grid scales with ZK, as well as an integrable discretization introduced here and a spectral discretization of KdV are not consistent with these hypotheses. On the contrary, for the ZK and an integrable finite-difference discretization of KdV, recurrence of a low-mode initial state is observed to be strongest and most persistent at an intermediate scale. We conclude that the observed recurrence is a lattice property and not a reflection of the integrable dynamics of KdV.

### 1. Introduction

When Zabusky and Kruskal [36] performed numerical simulations of the Korteweg–de Vries equation (KdV),

$$
(1.1)\quad u_t + u u_x + \delta^2 u_{xxx} = 0,
$$

with periodic boundary conditions \((u(0,t) = u(2,t))\), they were looking for the recurrence of the single-mode initial condition

$$
(1.2)\quad u(x,0) = \sin(\pi x), \quad 0 \le x \le 2,
$$

at regular time intervals. The recurrence of the initial condition was expected because, in this instance, KdV (1.1) was considered an asymptotic limit of the nonlinear oscillator lattice first investigated by Fermi, Pasta and Ulam (FPU) [15]. In addition to observing repeated (partial) recurrences, Zabusky and Kruskal also famously observed the elastic nonlinear interaction of localized waves and coined the term soliton to denote their particle-like coherence [36].

2010 Mathematics Subject Classification. Primary 34C60, 37J35. The second and third authors gratefully acknowledge support for this work by NSF DMS 1009517.

The story of the first investigations by FPU – as well as the follow-on discoveries by Kruskal, et al. – has been told many times, so it will not be repeated here. Moreover, the subsequent literature on both the FPU problem and KdV is too vast and varied to summarize adequately in this space. For our purposes, the essential elements are as follows: FPU considered their nonlinear lattice systems to be “toy” models of a general, macroscopic, physical system in which nonlinear terms cause interaction between the normal modes of the linear system (i.e., Fourier modes). In accordance with the postulates that underlie statistical derivations of macroscopic thermodynamics, FPU expected to see a single-mode initial condition evolve to a state in which the energy was evenly distributed across all the Fourier modes (“thermalization”). Instead, numerical simulations yielded repeated approximate recurrences of the single-mode initial state at evenly-spaced time intervals.

Given the discovery of recurrence by FPU and the derivation of KdV as an asymptotic model of the FPU lattice (cf. e.g., [31]), Zabusky and Kruskal did not identify recurrences observed in simulations of KdV [36] as a novelty. Instead, for Zabusky and Kruskal, the novel surprising result observed in simulations of KdV was the elastic interaction of solitons (in the approximate form of the classical sech² traveling-waves of KdV). The discovery of the solitons (more precisely, their elastic interactions) inspired the development of the Inverse-Scattering Transform (IST) method for the solution of KdV [16], which in turn led to the characterization of KdV as a completely integrable Hamiltonian system (cf. e.g., [13]). Despite the original suspicions of Kruskal [27], the theory of solitons and the IST is, of course, not uniquely applicable to KdV, and has been extended to a broad array of physically important and mathematically rich nonlinear evolution equations on the line (cf. e.g., [3]), as well as systems with periodic and quasiperiodic boundary conditions (cf. e.g., [11, 23, 29]).

The logical circle is completed by invoking the solitons of KdV as an explanation for the recurrence observed by Zabusky and Kruskal (e.g., [30, 36]). By extension, the recurrence observed in simulations of the FPU lattice is then explained on the grounds that FPU dynamics are governed by KdV (e.g., [8, 32]). Even at first glance, the connections are non-trivial: the individual sech² solitons, and multisoliton solutions, are solutions of KdV with vanishing boundary conditions on the whole line \((u \to 0 \text{ as } x \to \pm\infty)\), while solutions of KdV with periodic boundary conditions are more complex (cf. e.g., [11, 23, 29]). Nevertheless, if an individual soliton is narrow compared to the spatial period, the soliton does not “see” the periodic boundary condition and exists as an approximate solution (the limit of a periodic “cnoidal” wave). Indeed, the correspondence between periodic and whole-line solutions can be developed even for a spatially periodic solution whose support is not small compared to the spatial period [30]. Even so, the periodic boundary conditions are an important ingredient for the soliton view of recurrence: to achieve (approximate) recurrence, the unidirectional solitons of whole-line KdV “wrap around” in order to nearly recover their original arrangement as the system evolves.

The system integrated by Zabusky and Kruskal [36] was not, strictly speaking, KdV (1.1) itself, but rather the lattice (1.3)

$$
\frac{\mathrm{d}}{\mathrm{d}t} u_n = \frac{(u_{n-1}+u_n+u_{n+1})(u_{n-1}-u_{n+1})}{6h} + \delta^2 \frac{u_{n-2} - 2u_{n-1} + 2u_{n+1} - u_{n+2}}{2h^3}
$$

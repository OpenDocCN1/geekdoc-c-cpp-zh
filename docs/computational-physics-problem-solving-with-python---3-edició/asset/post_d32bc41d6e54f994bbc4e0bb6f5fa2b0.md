
19.4.1 Relaxation and Over-relaxation 469
19.4.2 Lattice PDE Implementation 470
19.5 Assessment via Surface Plot 471
19.6 Alternate Capacitor Problems 471
19.7 Implementation and Assessment 474
19.8 Electric Field Visualization (Exploration) 475
19.9 Review Exercise 476

## 20 Heat Flow via Time Stepping 477
20.1 Heat Flow via Time-Stepping (Leapfrog) 477
20.2 The Parabolic Heat Equation (Theory) 478
20.2.1 Solution: Analytic Expansion 478
20.2.2 Solution: Time Stepping 479
20.2.3 von Neumann Stability Assessment 481
20.2.4 Heat Equation Implementation 483
20.3 Assessment and Visualization 483
20.4 Improved Heat Flow: Crank–Nicolson Method 484
20.4.1 Solution of Tridiagonal Matrix Equations ⊙ 487
20.4.2 Crank–Nicolson Implementation, Assessment 490

## 21 Wave Equations I: Strings and Membranes 491
21.1 A Vibrating String 491
21.2 The Hyperbolic Wave Equation (Theory) 491
21.2.1 Solution via Normal-Mode Expansion 493
21.2.2 Algorithm: Time Stepping 494
21.2.3 Wave Equation Implementation 496
21.2.4 Assessment, Exploration 497
21.3 Strings with Friction (Extension) 499
21.4 Strings with Variable Tension and Density 500
21.4.1 Waves on Catenary 501
21.4.2 Derivation of Catenary Shape 501
21.4.3 Catenary and Frictional Wave Exercises 503
21.5 Vibrating Membrane (2D Waves) 504
21.6 Analytical Solution 505
21.7 Numerical Solution for 2D Waves 508

## 22 Wave Equations II: Quantum Packets and Electromagnetic 511
22.1 Quantum Wave Packets 511
22.2 Time-Dependent Schrödinger Equation (Theory) 511
22.2.1 Finite-Difference Algorithm 513
22.2.2 Wave Packet Implementation, Animation 514
22.2.3 Wave Packets in Other Wells (Exploration) 516
22.3 Algorithm for the 2D Schrödinger Equation 517
22.3.1 Exploration: Bound and Diffracted 2D Packet 518
22.4 Wave Packet–Wave Packet Scattering 518

## Contents
22.4.1 Algorithm 520
22.4.2 Implementation 520
22.4.3 Results and Visualization 522
22.5 E&M Waves via Finite-Difference Time Domain 525
22.6 Maxwell’s Equations 525
22.7 FDTD Algorithm 526
22.7.1 Implementation 530
22.7.2 Assessment 530
22.7.3 Extension: Circularly Polarized Waves 531
22.8 Application: Wave Plates 533
22.9 Algorithm 534
22.10 FDTD Exercise and Assessment 535

## 23 Electrostatics via Finite Elements 537
23.1 Finite-Element Method ⊙ 537
23.2 Electric Field from Charge Density (Problem) 538
23.3 Analytic Solution 538
23.4 Finite-Element (Not Difference) Methods, 1D 539
23.4.1 Weak Form of PDE 539
23.4.2 Galerkin Spectral Decomposition 540
23.5 1D FEM Implementation and Exercises 544
23.5.1 1D Exploration 547
23.6 Extension to 2D Finite Elements 547
23.6.1 Weak Form of PDE 548
23.6.2 Galerkin’s Spectral Decomposition 548
23.6.3 Triangular Elements 549
23.6.4 Solution as Linear Equations 551
23.6.5 Imposing Boundary Conditions 552
23.6.6 FEM 2D Implementation and Exercise 554
23.6.7 FEM 2D Exercises 554

## 24 Shocks Waves and Solitons 555
24.1 Shocks and Solitons in Shallow Water 555
24.2 Theory: Continuity and Advection Equations 556
24.2.1 Advection Implementation 558
24.3 Theory: Shock Waves via Burgers’ Equation 559
24.3.1 Lax–Wendroff Algorithm for Burgers’ Equation 560
24.3.2 Implementation and Assessment of Burgers’ Shock Equation 561
24.4 Including Dispersion 562
24.5 Shallow-Water Solitons: The KdEv Equation 563
24.5.1 Analytic Soliton Solution 563
24.5.2 Algorithm for KdEv Solitons 564
24.5.3 Implementation: KdEv Solitons 565
24.5.4 Exploration: Solitons in Phase Space, Crossing 567
24.6 Solitons on Pendulum Chain 567
24.6.1 Including Dispersion 568
24.6.2 Continuum Limit, the Sine-Gordon Equation 570
24.6.3 Analytic SGE Solution 571
24.6.4 Numeric Solution: 2D SGE Solitons 571
24.6.5 2D Soliton Implementation 573
24.6.6 SGE Soliton Visualization 574

## 25 Fluid Dynamics 575
25.1 River Hydrodynamics 575
25.2 Navier–Stokes Equation (Theory) 576
25.2.1 Boundary Conditions for Parallel Plates 578
25.2.2 Finite-Difference Algorithm and Overrelaxation 580
25.2.3 Successive Overrelaxation Implementation 581
25.3 2D Flow over a Beam 581
25.4 Theory: Vorticity Form of Navier–Stokes Equation 582
25.4.1 Finite Differences and the SOR Algorithm 584
25.4.2 Boundary Conditions for a Beam 585
25.4.3 SOR on a Grid 587
25.4.4 Flow Assessment 589
25.4.5 Exploration 590

## 26 Integral Equations of Quantum Mechanics 591
26.1 Bound States of Nonlocal Potentials 591
26.2 Momentum–Space Schrödinger Equation (Theory) 592
26.2.1 Integral to Matrix Equations 593
26.2.2 Delta-Shell Potential (Model) 595
26.2.3 Binding Energies Solution 595
26.2.4 Wave Function (Exploration) 597
26.3 Scattering States of Nonlocal Potentials ⊙ 597
26.4 Lippmann–Schwinger Equation (Theory) 598
26.4.1 Singular Integrals (Math) 599
26.4.2 Numerical Principal Values 600
26.4.3 Reducing Integral Equations to Matrix Equations (Method) 600
26.4.4 Solution via Inversion, Elimination 602
26.4.5 Scattering Implementation 603
26.4.6 Scattering Wave Function (Exploration) 604

Appendix A Codes, Applets, and Animations 607

Bibliography 609

Index 615

## Preface

Seventeen years have past since Wiley first published Landau and Páez’s *Computational Physics* and twelve years since Cristian Bordeianu joined the collaboration for the second edition. This third edition adheres to the original philosophy that the best way to learn computational physics (CP) is by working on a wide range of projects using the text and the computer as partners. Most projects are still constructed using a computational, scientific problem-solving paradigm:

Problem → Theory/Model → Algorithm ↔ Visualization ↺    (0.1)

Our guiding hypothesis remains that CP is a computational science, which means that to understand CP you need to understand some physics, some applied mathematics, and some computer science. What is different in this edition is the choice of Python for sample codes and an increase in the number of topics covered. We now have a survey of CP which is more than enough for a full-year’s course.

The use of Python is more than just a change of language, it is taking advantage of the Python ecosystem of base language plus multiple, specialized libraries to provide all computational needs. In addition, we find Python to be the easiest and most accessible language for beginners, while still being excellent for the type of interactive and exploratory computations now popular in scientific research. Furthermore, Python supplemented by the Visual package (VPython) has gained traction in lower division physics teaching, and this may serve as an excellent segue to a Python-based CP course. Nevertheless, the important aspects of computational modeling and thinking transcends any particular computer language, and so having a Python alternative to our previous use of Fortran, C and Java may help promote this view (codes in all languages are available).

As before, we advocate for the use of a compiled or interpreted programming language when learning CP, in contrast to a higher level problem-solving environment like Mathematica or Maple, which we use in daily work. This follows from our experiences that if you want to *understand* how to compute scientifically, then you must look inside a program’s black box and get your hands dirty. Otherwise, the algorithms, logic, and the validity of solutions cannot be ascertained, and that is not a good physics. Not surprisingly, we believe all physicists should know how to read programs how to write them as well.

Notwithstanding our beliefs about programming, we appreciate how time-consuming and frustrating debugging programs often is, and especially for beginners. Accordingly, rather than make the learner write all codes from scratch, we have placed a large number of codes within the text and often ask the learner only to run, modify, and extend them. This not only leaves time for exploration and analysis, but also provides experience in the modern work environment in which one must incorporate new developments into the preexisting codes of others. Be that as it may, for this edition we have added problems in which the relevant codes are not in the text (but are available to instructors). This should permit an instructor to decide on the balance of new and second-hand codes with which their students should work.

In addition to the paper version of the text, there is also an eBook of it that incorporates many of the multimodal enhancements possible with modern technologies: video lecture modules, active simulations, editable codes, animations, and sounds. The eBook is available as a Web (HTML5) document appropriate for both PCs or mobile devices. The lecture modules, which can be viewed separately from the eBook, cover most of the topics in the text, are listed in Appendix B, and are available online. They may provide avenues for alternative understanding the text (either as a preview or a review), for an online course, or for a blended course that replaces some lecture time with lab time. This latter approach, which we recommend, provides time for the instructor to assist students more personally with their projects and their learning issues. The studio-produced lectures are truly “modules,” with active slides, a dynamic table of context, excellent sound (except maybe for a Bronx accent), and with occasional demonstrations replacing the talking head.

The introductory chapter includes tables listing all of the problems and exercises in the text, their locations in the text, as well as the physics courses in which these problems may be used as computational examples. Although we think it better to have entire courses in CP rather than just examples in the traditional courses, the inclusion of examples may serve as a valuable first step towards modernization.

The entire book has been reedited to improve clarity and useability. New materials have also been added, and this has led to additional and reorganized chapters. Specific additions not found in the second edition include: descriptions of the Python language and its packages, demonstrations of several visualization packages, discussions of algebraic tools, an example on protein folding, a derivation of the Gaussian quadrature rule, searching to obtain the temperature dependence of magnetization, chaotic weather patterns, planetary motion, matrix computing with Numerical Python, expanded and updated discussion of parallel computing including scalability and domain composition, optimized matrix computing with NumPy, GPU computing, CUDA programming, principal components analysis, digital filtering, the fast Fourier transform (FFT), an entire chapter on wavelet analysis and data compression, a variety of predator–prey models, signals of chaos, nonlinear behavior of double pendulum, cellular automata, Perlin noise, ray tracing, Wang–Landau sampling for thermodynamic simulations, fi-

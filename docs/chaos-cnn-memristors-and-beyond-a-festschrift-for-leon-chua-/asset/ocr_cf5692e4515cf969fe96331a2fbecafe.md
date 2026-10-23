the main featuresᵃ of a chaotic system — sensitivity to initial conditions, aperiodicity and boundedness of trajectories. His 1963 paper was related to work he initially did in 1961 at the Travelers Insurance Company Weather Center in Hartford, Connecticut. Lorenz was shown a 7-equation model of fluid convective motion. Lorenz simplified this model into a 3-equation system of nonlinear Ordinary Differential Equations (ODEs), shown in Eqs. (1) through (3).

```
ẋ = −σx + σy  (1)
ẏ = −xz + ρx − y  (2)
ż = xy − βz  (3)
```

The dot notation has been used to indicate a derivative with respect to time and will be employed throughout this chapter. For σ = 10, β = 8/3, Lorenz observed via computer simulations that the system behaved “chaotically” whenever ρ exceeded the approximate critical value of 24.74. A phase plot (x(t), y(t), z(t)) obtained from numerical simulation of Eqs. (1) through (3) has been plotted in Fig. 1. The system equations have been numerically simulated and rendered using Mathematica 8 [20]. All calculations were also performed using Mathematica. The Mathematica source for this chapter can be found online at http://myweb.msoe.edu/muthuswamy/MuthuswamyWSPC2011ChuaBook-OnlineFiles/.

Although Lorenz’s clever geometric arguments [10] implied that chaos in Eqs. (1) through (3) was not a mathematical anomaly, no one could reproduce chaos physically in the 1970s and early 1980s. Thus, in order to verify that steady-state chaotic behavior was not an artifact of computer simulations, there was a need for a physical chaotic system. One of the main reasons for the lack of a physical realization of early chaotic systems such as Lorenz and Rössler’s equations [16] was the presence of multiplier terms in the nonlinearities. These terms were hard to realize physically, especially electronically since the analog multiplier did not become a reliable electronic component [5] till the late 1980s.

The lack of a physical realization would change in 1983, twenty years after Lorenz’s paper, when

![](bbox=[0.52, 0.09, 0.92, 0.42])

Fig. 1. The Lorenz butterfly. It is also called as a “chaotic attractor” because the underlying system exhibits chaotic behavior and nearby initial conditions are “attracted” into the butterfly. The attractor trajectory has been colored to highlight the unique shape in three dimensional space.

Leon O. Chua systematically derived Chua’s circuit. Because of the systematic derivation, Chua’s circuit utilized piecewise-linear nonlinearities as opposed to product terms. Hence physical realization of Chua’s circuit and a rigorous proof of chaos would only take a total of two years [5]. In contrast the first electronic realization of Lorenz’s system [18] was done, interestingly enough, using piecewise linear approximations to the product terms in 1989. Rigorous proof of chaos in the Lorenz system [19] would only be published in 1999, thirty six years after Lorenz’s seminal work.

The rest of this chapter will study some of the most important properties of Chua’s circuit. First we will systematically design and realize Chua’s circuit [11]. Next we will emphasize why a rigorous proof of chaos is necessary and outline the approach for proving rigorous existence of chaos in Chua’s circuit. This section will serve as a “cookbook” for the reader in proving rigorous existence of chaos in piecewise-linear systems. We emphasize piecewise-linear systems because Sec. 4 will provide

ᵃWe want to emphasize these features are not the definition of a chaotic system. To understand why no definition of chaos presently exists, please refer to [3].
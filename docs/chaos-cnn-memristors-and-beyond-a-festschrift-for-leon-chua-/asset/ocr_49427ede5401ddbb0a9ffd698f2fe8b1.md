![](bbox=[0.17, 0.09, 0.44, 0.28])

![](bbox=[0.54, 0.09, 0.81, 0.28])

Fig. 12. (a) The comparison of i(t) between the Volterra result (dashed) and the numerical curve (solid). (b) The Volterra series of the fourth order provides good results for the amplitudes up to the fourth harmonic.

second by the Volterra based single memristor circuit approach.

In Fig. 11, the pinched hysteresis loop of the result obtained numerically is compared to the Volterra series based result, which has been determined by taking into account terms up to Volterra order four. It confirms the high approximation accuracy of the Volterra approach. The power spectrum of the output function is presented in Fig. 12. Up to the 4th harmonic, the Volterra amplitudes show a maximal relative error of 0.3% as compared to the numerically calculated amplitudes. In general, we can expect the Volterra ansatz providing good approximations for the higher harmonics up to the highest Volterra order which we take into account in the analytical calculation.

The parameter m₁ is a measure for the strength of the nonlinearity of the system. In the calculation, we used m₁ = 9.1·10⁵ Ω/C which is the highest value of m₁ that leads to a steady state output. Increasing the value of m₁ further, forces the memristor into a state of being an energy source. Thus, the current i₂ and the voltage u₂ will finally diverge. Hence we can conclude for the considered circuit that in all cases with steady states, the Volterra approach provides an excellent approximation.

A second example and the corresponding results are given in Figs. 13 and 14. In this case, there are four dynamic devices and we have four independent states. As in the previous example, the time dependent circuit quantities which are calculated by means of the derived Volterra Kernels, are in good agreement with their corresponding numerical values.

![](bbox=[0.52, 0.39, 0.88, 0.53])

Fig. 13. Another example circuit with three branches and four dynamic devices. Parameters: ω = 200 Hz, L = 5mH, C₁ = 2μF, C₂ = 1μF, R₁ = 1kΩ, R₂ = 100Ω, m₀ = 2kΩ, m₁ = 0.83·10⁶ Ω/C.

# 5. Conclusions

In this chapter we have introduced two methods for the analysis of circuits with memristors. The multilinear method proved to deliver good results for several circuits with a given structure while the Volterra series based approach describes the behavior of a class of memristor circuits. We introduced the class of SMC and provided an analytical solution for this class in the form of (21)–(25). The derived equations can be adapted easily to other circuit forms (e.g. when the linear system is given by its admittance matrix) and other input-output quantities. Provided a unique steady state, the described Volterra based SMC analysis is quite general and hence gives the possibility to investigate SMC systematically. The influence of circuit parameters (e.g. a capacity value) on the output properties can hence be studied analytically without the need to carry out numerical simulations for
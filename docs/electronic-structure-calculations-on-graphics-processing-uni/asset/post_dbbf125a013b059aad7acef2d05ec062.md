
### Timings and speed-up for the analytical frequency calculation

![](img/255d48531d66773aa863436a333dac7d_140_0.png)

Figure 5.4 Timings and speed-up for the calculation of Hessian matrix elements for an analytical frequency calculation on the budesonide molecule (C$_{25}$H$_{34}$O$_4$) using B3LYP/TZ2P and frozen core setting “small” using a Becke grid quality of “good” in ADF.

Figure 5.4 shows the timings and speedup for an analytical frequency calculation on the budesonide molecule (C$_{25}$H$_{34}$O$_4$) using a TZ2P basis set. The GGA BLYP functional, the frozen cores “small” setting, and a Becke grid quality “good” in ADF. The calculation is performed for only 3 of the 65 atoms, creating a partial Hessian, and Figure 5.4 shows only the timings for the loop over the atomic nuclei, because this loop will take ~98% of the total calculation time for a full Hessian. The timings are thus representative for a full frequency calculation. Figure 5.4 shows a 2.16x speedup when using only 2 CPU cores (6 CPU cores per GPU), and a 1.70x speedup when using 12 CPU cores (6 cores per GPU).

The calculations in the frequencies code are accelerated using the same hybrid scheme as explained in Section 5.3.3. The only difference is the ratio between numerical integration and calculation of the operator and basis function (derivative) values on the grid, which is ~4:1 for the flu1_a1_gqa routine. This gives a possible speedup factor of 5, which is slightly higher when compared to the flocky routine. However, the number of CPU cores that share a GPU needs to be low; otherwise the numerical integration cannot be hidden behind CPU work, reducing the possible speedup.

The timings and speedup of the flu1_a1_gqa routine are shown in Figure 5.5. When only two CPU cores are used, all numerical integration work performed on the two GPUs is hidden behind other CPU work, giving a 4.43x speedup. The estimated 5x possible speedup is not achieved because of the increased overhead of the wrapper routine, which reorders the input arrays on the CPU before sending them to the GPU. This is necessary to enable coalesced data fetches from global memory in the numerical integration kernel, something that is otherwise difficult to achieve with the current data structure used in the ADF gradients code. The speedup reduces to 2.66x when using 12 CPU cores, showing that there is still room for improvement with the current GPU acceleration scheme.

Bringing the auxiliary matrix scheme to GPU would be a good way to reduce the number of operations required in each integration grid batch and at the same time solve the data structure problem.

### Timings and speed-up for the f1u1_ai_gaa routine

![](img/255d48531d66773aa863436a333dac7d_141_0.png)

**Figure 5.5** Timings and speed-up for the calculation of matrix elements of the Fock matrix derivatives (routine f1u1_ai_gaa) required for analytical frequency calculation. Test system is the budesonide molecule (C25H34O5) with B3LYP/TZ2P and frozen core setting “small”, using a Becke grid quality of “good” in ADF

## 5.4 Conclusion

DFT calculations with STOs as implemented in the ADF software package were accelerated using a low-latency CUDA kernel for the numerical integration of Fock matrix elements, aimed at obtaining good performance for relatively small problem sizes. The kernel achieved almost 50% of the DGEMM performance on the Tesla Fermi architecture (134 GFLOPS), and was portable enough to run twice as fast on K20 (262 GFLOPS) and thrice faster on K40 (408 GFLOPS).

A hybrid computational model was developed to offload the heavy numerical work to the GPU, keeping the CPU working at the same time. The balance in workload between CPU and GPU causes the numerical integration bottleneck to disappear if the number of CPU cores per GPU is not too large. The accelerated ADF code was shown to be 1.45–1.89 times faster for single-point calculations, depending on the grid accuracy settings, and 1.70–2.16 times faster for frequency calculations, depending on the ratio of CPU cores to GPU devices.

Software packages with a large amount of legacy code, such as ADF, can be difficult targets for GPU acceleration, as it is impossible to port them entirely to GPUs within a reasonable amount of time. The hybrid scheme described here can be a good solution for such cases, offering decent speedup without sacrificing any of the features that make the code unique.

GPU acceleration in ADF is work in progress with plenty of room for improvement. In the near future, we hope to optimize the frequencies code and extend the acceleration to functionals beyond GGAs and other property calculations.

## References

- 1. Kohn, W., Becke, A.D. and Parr, R.G. (1996) Density functional theory of electronic structure. Journal of Physical Chemistry A, 100 (31), 12974–12980.
- 2. Neese, F. (2009) Prediction of molecular properties and molecular spectroscopy with density functional theory: From fundamental theory to exchange-coupling. Coordination Chemistry Reviews, 253 (5–6), 526–563.
- 3. Cohen, A.J., Mori-Sánchez, P. and Yang, W. (2012) Challenges for density functional theory. Chemical Reviews, 112 (1), 289–320.
- 4. Kutzelnigg, W. (2013) Expansion of a wave function in a Gaussian basis. I. Local versus global approximation. International Journal of Quantum Chemistry, 113 (3), 203–217.
- 5. Güell, M., Luis, J.M., Solà, M. and Swart, M. (2008) Importance of the basis set for the spin-state energetics of iron complexes. Journal of Physical Chemistry A, 112 (28), 6384–6391.
- 6. ADF2013, SCM, Theoretical Chemistry, Vrije Universiteit, Amsterdam, The Netherlands, http://www.scm.com (accessed 07 September 2015).
- 7. Te Velde, G., Bickhaupt, F.M., Baerends, E.J. et al. (2001) Chemistry with ADF. Journal of Computational Chemistry, 22 (9), 931–967.
- 8. Fonseca Guerra, C., Snijders, J., Te Velde, G. and Baerends, E. (1998) Towards an order-N DFT method. Theoretical Chemistry Accounts, 99 (6), 391–403.
- 9. Atkins, P.J. (2004) Essentials of Computational Chemistry: Theories and Models, John Wiley & Sons, p. 628.
- 10. Jensen, F. (2007) Introduction to Computational Chemistry, 2nd edn, John Wiley & Sons, Chichester.
- 11. Fonseca Guerra, C., Visser, O., Snijders, J.G. te Velde, G. and Baerends, E.J. (1995) Parallelisation of the Amsterdam Density Functional Program. In: Methods and Techniques for Computational Chemistry, E. Clementi and C. Corongiu, eds. pp. 303–395, STEF, Cagliari. http://www.scm.com/Doc/metccc.pdf.
- 12. Wolf, S.K. (2005) Analytical second derivatives in the Amsterdam density functional package. International Journal of Quantum Chemistry, 104 (5), 645–659.
- 13. Nicu, V.P., Neugebauer, J., Wolff, S.K. and Baerends, E.J. (2008) A vibrational circular dichroism implementation within a Slater-type-orbital based density functional theory framework and its application to hexa- and hepta-helicenes. Theoretical Chemistry Accounts, 119 (1-3), 245–263.
- 14. Franchini, M., Philipsen, P.H.T. and Visscher, L. (2013) The Becke fuzzy cells integration scheme in the Amsterdam density functional program suite. Journal of Computational Chemistry, 34 (21), 1819–1827.
- 15. Volkov V. 2010 Better performance at lower occupancy. Proceedings of the GPU Technology Conference. GTC, http://people.cs.fsu.edu/~gerlebacher/gpus/better_performance_at_lower_occupancy_gtc2010_volkov.pdf.

## 6 Wavelet-Based Density Functional Theory on Massively Parallel Hybrid Architectures

Luigi Genovese¹, Brice Videau², Damien Caliste¹, Jean-François Méhaut², Stefan Goedecker³ and Thierry Deutsch¹

¹Université Grenoble Alpes, INAC, F-38000 Grenoble, France, and CEA, INAC, F-38000 Grenoble, France
²Université Joseph Fourier – Laboratoire d’Informatique de Grenoble – INRIA, Grenoble, France
³Institut für Physik, Universität Basel, Basel, Switzerland

In this chapter, we describe the GPU acceleration of density functional theory (DFT) calculations based on wavelet basis sets as realized in the BigDFT code. Daubechies wavelets have not been traditionally used for DFT calculations, but we exhibit properties that make them attractive for both accurate and efficient DFT simulations. Here we explain how an existing MPI parallel wavelet-based DFT implementation can benefit from the computational power of GPUs by offloading numerically intensive operations to GPUs.

### 6.1 Introductory Remarks on Wavelet Basis Sets for Density Functional Theory Implementations

Quantum mechanics and electromagnetism are widely perceived as leading to a “first-principles” approach to materials and nanosystems: given appropriate software implementations and sufficiently powerful hardware, it is possible to calculate properties without resorting to any adjustable parameters. In the 1980s, it became clear that, indeed, numerous material properties such as total energies, electronic structure, and the related dynamic, dielectric, mechanical, magnetic, and vibrational properties, can be obtained with an accuracy that can be considered as truly predictive.

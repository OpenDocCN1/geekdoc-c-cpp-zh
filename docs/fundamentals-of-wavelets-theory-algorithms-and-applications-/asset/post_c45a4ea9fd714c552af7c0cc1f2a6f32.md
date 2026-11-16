
- 26. J. Morlet, G. Arens, E. Fourgeau, and D. Girard. “Wavelet Propagation and Sampling Theory. Part II, Sampling Theory and Complex Waves.” Geophysics 47 (1982), 222–236.

- 27. G. J. Moridis, M. Nikolaou, and Y. You. “The Use of Wavelet Transforms in the Solution of Two-Phase Flow Problems.” SPE J. (1996), 169–177.

- 28. P. Kumar and E. Foufoula-Georgiou. “Wavelet Analysis for Geophysical Applications.” AGU Rev. Geophys. 35(4) (November 1997), 385–412.

- 29. L. Chu, R. A. Schatzinger, and M. K. Tham. “Application of Wavelet Analysis to Upscaling of Rock Properties.” SPE Reservoir Eval. Eng. (February 1998), 75–81.

- 30. G. Bernasconi, V. Rampa, F. Abramo, and L. Bertelli. “Compression of Downhole Data.” SPE/IADC 52806, 1999.

- 31. F. González-Tamez, R. Camacho-Velázquez, and B. Escalante-Ramirez. “Truncation De-Noising in Transient Pressure Tests.” SPE #56422, 1999.

- 32. M. N. Panda, C. C. Mosher, and A. K. Chopra. “Application of Wavelet Transforms to Reservoir-Data Analysis and Scaling.” SPE J. (March 2000), 92–101.

- 33. P. Lu, and R. N. Horne. “A Multiresolution Approach to Reservoir Parameter Estimation Using Wavelet Analysis.” SPE 62985, October 2000.

- 34. M. Y. Soliman, J. Ansah, S. Stephenson, and B. Mandal. “Application of Wavelet Transform to Analysis of Pressure Transient Data.” SPE J. (71571) 2001.

- 35. S. Ray and A. K. Chan. “Automatic Feature Extraction from Wavelet Coefficients Using Genetic Algorithms.” Paper presented at the IEEE Signal Processing Society Workshop, Falmouth, MA, September 2001.

- 36. S. Athichanagorn, R. N. Horne, and J. Kikani. “Processing and Interpretation of Long-Term Data Acquired from Permanent Pressure Gauges.” SPE Reservoir Eval. Eng. (October 2002), 384–391.

- 37. A. Grinsted, J. C. Moore, and S. Jevrejeva. “Application of the Cross Wavelet Transform and Wavelet Coherence to Geophysical Time Series.” Nonlinear Proc. Geophys (2004), 561–566.

- 38. N. Bennett and A. Malinverno. “Fast Model Updates Using Wavelets.” SIAM J. Multiscale Modeling Simulation 3 (2004), 106–130.

- 39. N. A. Rivera, S. Ray, J. L. Jensen, A. K. Chan, and W. B. Ayers. “Detection of Cyclic Patterns Using Wavelets: An Example Study in the Ormskirk Sandstone, Irish Sea.” Math. Geol. 36 (July 2004), 529–543.

- 40. L. Guan, Y. Du, and L. Li. “Wavelets in Petroleum Industry: Past, Present, and Future,” SPE 89952, October 2004.

- 41. I. Sahni and R. N. Horne. “Multiresolution Wavelet Analysis for Improved Reservoir Description.” SPE Reservoir Eval. Eng. 3 (February 2005), 53–69.

- 42. G. Hennefent and F. J. Herrmann. “Seismic Denoising with Nonuniformly Sampled Curvelets, IEEE Comput. Sci. and Eng. (May/June 2006), 16–25.

- 43. W. Yue, G. Tao, and Z. Liu. “Identifying Reservoir Fluids by Wavelet Transform of Well Logs.” SPE Reservoir Eval. Eng. (October 2006), 574–581.

- 44. P. P. Moghadam, F. Herrmann, and C. Stolk. “Migration Amplitude Recovery Using Curvelets.” CSPG CSEG Convention (2007), 409–413.

- 45. D. Viberti, F. Verga, and P. Delbosco. “An Improved Treatment of Long-Term Pressure Data for Capturing Information.” SPE Reservoir Eval. and Eng. (August 2007), 359–366.

- 46. V. Kumar and F. Herrmann. “Curvelet-Regularized Seismic Deconvolution.” CSPG CSEG CWLS Convention (2008), 311–314.

- 47. P. M. Ribeiro, A. P. Pires, E. A. P. Oliveira, and J. G. Ferroni. “Use of Wavelet Transform in Pressure-Data Treatment.” SPE Prod. Operation (February 2008), 24–31.

- 48. J. C. Goswami, D. Heliot, J. Tabanou, and D. Allen. “Determination of Regional Dip and Formation Properties from Log Data in a High Angle Well.” Petrophysics 49 (June 2008), 295–300.

- 49. C. E. P. Ortiz, R. B. Aguiar, and A. P. Pires. “Wavelet Filtering of Permanent downhole Gauge Data.” SPE 123028, 2009.

- 50. A. Gholami and H. R. Siahkoohi. “Regularization of Linear and Non-Linear Geophysical Ill-Posed Problems with Joint Sparsity Constraints.” Geophys. J. Int. 180 (February 2010), 871–882.

## CHAPTER TEN

### Wavelets in Boundary Value Problems

All of the applications discussed so far deal with processing a given function (signal, image, etc.) in the time, frequency, and time-frequency domains. We have seen that wavelet-based time-scale analysis of a function can provide either additional information that cannot be obtained by either time or frequency domain analyses. There is another class of problems that we quite often come across involve solving boundary value problems (BVPs). In BVPs functions are not known explicitly; some of their properties along with function values are known at a set of certain points in the domain of interest. In this chapter we discuss the applications of wavelets in solving such problems.

Much of the phenomena studied in electrical engineering can be described mathematically by second-order partial differential equations (PDEs). Some examples of PDEs are the Laplace, Poisson, Helmholtz, and Schrödinger equations. Each of these equations may be solved analytically for some but not for all cases of interest. These PDEs can often be converted to integral equations. One of the attractive features of integral equations is that boundary conditions are built-in and, therefore, do not have to be applied externally [1]. Mathematical questions of existence and uniqueness of a solution may be handled with more ease with the integral form.

Either approach, differential or integral equations, to represent a physical phenomenon can be viewed in terms of an operator operating on an unknown function to produce a known function. In this chapter we deal with the linear operators. The linear operator equation is converted to a system of linear equations with the help of a set of complete bases, which is then solved for the unknown coefficients. The finite element and finite difference techniques used to solve PDEs result in sparse and banded matrices, whereas integral equations almost always lead to a dense matrix. An exception is when the basis functions, chosen to represent the unknown functions, happen to be the eigen functions of the operator.

Two of the main properties of wavelets vis-à-vis boundary value problems are their hierarchical nature and the vanishing moments properties. Because of their hierarchical (multiresolution) nature, wavelets at different resolutions are interrelated, a property that makes them suitable candidates for multigrid-type methods in solving PDEs. On the other hand, the vanishing moment property by virtue of which wavelets, when integrated against a function of certain order, make the integral zero, is attractive in sparsifying a dense matrix generated by an integral equation.

A complete exposition of the application of wavelets to integral and differential equations is beyond the scope of this chapter. Our objective is to provide readers with some preliminary theory and results on the application of wavelets to boundary value problems and give references where more details may be found. Since most often in electrical engineering problems we encounter integral equations, we emphasize their solutions using wavelets. We give a few examples of commonly occurring integral equations. The first and the most important step in solving integral equations is to transform them into a set of linear equations. Both conventional and wavelet-based methods in generating matrix equations are discussed. Both the methods fall under the general categories of method of moments (MoM). We call methods with conventional bases (pulse, triangular, piecewise sinusoid, etc.) conventional MoM, while methods with wavelet bases will be referred to as wavelet MoM. Some numerical results are presented to illustrate the advantages of the wavelet-based technique. We also discuss wavelets on a bounded interval. Some of the techniques applied to solving integral equations are useful for differential equations as well. At the end of this chapter we briefly describe the applications of wavelets in PDEs, particularly the multiresolution time domain (MRTD) method, and provide references where readers can find further information.

### 10.1 INTEGRAL EQUATIONS

Consider the following first-kind integral equation

```
\int_{a}^{b} f(x') K(x, x') dx' = g(x), \quad (10.1)
```

where f is the unknown function, and the kernel K and the function g are known. This equation, depending on the kernel and the limits of integration, is referred to by different names, such as Fredholm, Volterra, convolution, Laplace, Fourier, Hankel, Mellin, and Wiener-Hopf

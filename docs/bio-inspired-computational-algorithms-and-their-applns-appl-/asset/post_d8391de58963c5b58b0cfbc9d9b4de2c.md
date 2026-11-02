
![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_175_0.png)

Fig. 1. Results from Dullemond et al. (2001) model applied to the star AB Aurigae. The Synthetic SED is the sum of its components: star emission (continuous thin line); rim emission (dashed line); disc cold layer emission (dot-dashed line); and the disc hot layer emission (dotted line). The observational data in various wavelengths is represented by squares (Hetem & Gregorio-Hetem 2007).

### 3.1.2 Implementation

The GA code was designed and built to find the best disk parameters, namely S = {R_D, M_D, θ, p, T_rim, d, M_*, L_*, T_*}, as discussed in subsection 2.1. However, some of these parameters are already known: the stellar parameters d, L_*, and T_* are adopted from observations and easily found in literature. Essentially, the GA method used implements a χ² minimization of the SED fitting provided by the Dullemond et al. (2001) model. The main structures used to manipulate the data are linked lists containing the solutions (parameter set, adaptation level, χ²_i, and the genetic operator, Φ_i), expressed by

S_i = { {R_Di, θ_i, M_Di, p_i, T_i}, {χ²_i, Φ_i} } (1)

where S_i denotes the ith solution, and T_i is the ith Trim. Following Goldberg (1989), the code starts with the construction of the first generation, where all parameters are randomly chosen within an allowed range (for example, 50 ≤ RD ≤ 1000 AU). We chose as the number of individuals (parameter sets) in all the generations to be 100. In the following iteration loops, the evaluation function runs the Dullemond et al. (2001) model for each individual, and compares the synthetic SED with the observed data through a χ² measure, using the modified expression (Press et al. 1995):

χ²_i = 1/N Σ_{j=1}^N (F_j - φ_{ij})² (2)

where F_j is the observed flux at wavelength λ_j, N is the number of observed data points, and φ_{ij} is the calculated flux for the solution S_i. The smallest χ² is assumed to be the gof, the goodness-of-fit measure for that generation. The evaluation function is applied to all individuals, and then the judgement procedure sorts the list by increasing χ². It also sets one hundred random pairs of disc mass and radius around the parameters for the AB Aurigae model taken from Dominik et al. (2003). The result at the minimum is gof ~ 0.046, which means that the error bar estimation converged to a narrow range around the parameter set.

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_177_0.png)

Fig. 3. Contour levels gof(M_D, R_D) estimated for AB Aurigae presenting the confidence levels χ²(68%)=0.082 (continuous line), χ²(90%)=0.15 (dashed) and χ²(99%)=0.21 (dot–dashed) (Hetem & Gregorio-Hetem 2007).

We also applied the described GA method to four other stars, in order to verify the quality of the fitting for objects showing different SED shapes and different levels of infrared excess. Our set was chosen by the slope of their near-infrared SED. The infrared excess in Herbig Be stars is the result of a spherical dusty envelope (van den Ancker et al. 2001), whereas a thick-edge flared disc is characteristic of Herbig Ae. With this in mind, we selected A-type or late-B-type stars from the Pico dos Dias Survey sample (Gregorio-Hetem et al. 1992; Torres et al. 1995; Torres 1998) to apply the GA SED fitting. The results are presented in table 1 together with their corresponding gofs (see figure 4).

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_177_1.png)

Fig. 4. GA SEDs obtained for the stars BD-14 1319, IRAS 07394-1953, IRAS 06475-0735 and HD 141569. The plots are given as log[F_ν(Wm⁻²)] versus log[λ(μm)] (Hetem & Gregorio-Hetem 2007).

| PDS | Name | M_* (M⊙) | R_D (AU) | M_D (M⊙) | T_in (K) | θ (°) | p | gof |
|---|---|---|---|---|---|---|---|---|
| 398 | HD 141569 | 2.4 | 13 | 0.06 | 1085 | 0.6 | -2.0 | 0.006 |
| 022 | BD-14 1319 | 2.8 | 690 | 0.003 | 380 | 40 | -1.0 | 0.006 |
| 130 | IRAS 06475-0735 | 2.0 | 309 | 0.20 | 1705 | 53 | -1.5 | 0.016 |
| 257 | IRAS 07394-1953 | 2.0 | 859 | 0.64 | 1838 | 47 | -2.0 | 0.098 |

Table 1. Obtained parameters for the chosen stars (Hetem & Gregorio-Hetem 2007).

## 3.2 Abundances and Metallicities of young stars via Spectral Synthesis

This subsection is based on the published work The use of Genetic Algorithms and Spectral Synthesis in the Calculation of Abundances and Metallicities of T Tauri stars (Hetem & Gregorio-Hetem 2009).

In the previous subsection, we presented a method that uses a calculation technique based on GA aiming to optimize the parameters estimation of protoplanetary disks of T Tauri stars. Inspired by the success of that application, which gives accurate and efficient calculations, we decided to develop a similar method to determine atomic stellar abundances.

### 3.2.1 Artificial spectra as a measurement tool

In astrophysics, the absorption spectra are obtained and employed as an analytical chemistry tool to determine the presence of atoms and ions in stellar atmospheres and, if possible, to quantify the amount of the atoms present. In stellar atmospheres, each element produces a number of spectrum absorption lines, at wavelengths which can be measured with extreme accuracy when compared to spectra emission tables provided by laboratory experiments.

The presence of a given element in the star atmosphere can be verified (and measured) by looking for its absorption lines at the correct wavelength. The hydrogen is present in all stars by its Balmer absorption lines, and is often used to calibrate the measurements. An example of a high-resolution spectrum is presented in figure 5.

The way astrophysicists use to calculate the abundances of atoms in stars follows the steps:

- 1. Obtain the star spectrum in a given range (or ranges) of wavelength, where the lines of the elements in study should be;
- 2. Generate an artificial spectrum, considering the lines whose origin are the desired elements and the known physics of absorption line production;
- 3. Compare the artificial and observed spectra. Here a simple χ² test is enough to compute a general comparison index;
- 4. Use a GA methodology to optimize the artificial spectrum in order to minimize the differences with the observed spectrum (the inverted problem, subsection 2.1);
- 5. Once the optimization methodology reaches its goals, consider the elemental parameters (density, temperature, ionization, etc) as the measures of the elements in the stellar atmospheres.

### 3.2.2 Inverting the problem

From our discussion on section 2, one can see that generating a synthetic spectrum is a P-problem, as the result is obtained from a set of parameters, and no more computing is needed. The generation time is obviously finite, and there are a number of very efficient software tools that do that. The only care to be taken is to assure that the artificial spectrum has the same wavelength resolution of the observed spectrum, in order to simplify the future comparison.

The above mentioned step 4, a methodology to optimize the artificial spectrum, is the trick point. If one wants to use GA to solve the abundances problem, it is necessary to invert the P-problem, that is, it is necessary to use the artificial spectrum generation tool as an external routine of a bigger and more complex algorithm. The algorithm used to this task is presented in figure 6.

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_179_0.png)

Fig. 5. FEROS spectrum for star PDS054 (Rojas et al. 2008).

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_179_1.png)

Fig. 6. Main blocks of a GA code to fit multi-band spectra of T Tauri stars (adapted from Hetem & Gregorio-Hetem 2009).

Establishing the abundances of each element as the parameters to be found, one individual in the GA terminology is the set of all elemental abundances added to some atmospheric parameters. The initial parameter set is used to build the first generation with 100 individuals. The evaluator routine creates a synthetic spectrum whose entries are the genetic data in each chromosome. This task is performed by calling the elected spectral tool.

There are a number of very efficient software tools that can be chosen. In our application, the abundances of chemical species are determined by using the spectral synthesis software SPECTRUM provided by Corbally (Gray & Corbally 1994) and the atmosphere model software ATLAS9 from Kurucz (1993).

### 3.2.3 Results

In this section we present the results of the GA method for three stars, whose high-resolution spectra were obtained at European Southern Observatory (ESO) in La Silla, Chile, with the Fiber Extended Range Optical Spectrograph (FEROS) at the 1.52m telescope. The stellar parameters (effective temperature and gravity) were calculated by excitation and ionization equilibrium of iron absorption lines (Rojas et al. 2008). The atomic and molecular line data were mainly from the National Institute of Standards and Technology¹ and the Kurucz site². The solar atomic abundances are from Grevesse & Sauval (1998), and the hyperfine structure constants were taken from Dembczynski et al. (1979) and Luc & Gerstenkorn (1972). The atmosphere models were obtained from the Kurucz library. Specific atmosphere models were calculated through a GNU-Linux porting of the ATLAS9 program (Kurucz 1993).

¹ http://physics.nist.gov/PhysRefData/ASD/index.html
² http://kurucz.harvard.edu 4 and http://wwwuser.oat.ts.astro.it/castelli/

The method performs a multi-range fitting of specific regions of the observed spectrum, looking for best fit. The demands and commands to SPECTRUM are only those for generating the specific regions of interest, but the χ² comparing index is evaluated over all wavelength ranges. Figures 7 and 8 present the results for some stars on chosen lines.

The metallicities and abundances found for the stars are compatible with those previously obtained for this particular sample. These preliminary results, achieved by using the GA technique, indicate the efficiency of the method. In the future, we intend to use the method in a larger sample of T Tauri stars.

## 4. Applications on Rocket Engine engineering

This section presents two solutions in applying GAs in the aerospace area, both concerning the fuel pumping in liquid propellant rocket engines. There are many choices to be done in the design of a high performance fuel pump, being one of them the type of pump.

Two different types of pumps were modelled: the Harrington pumps and the turbo pumps. Both present a complex design methodology, which includes: tabled functions interpolations, numerical integrals and constructive material choices.

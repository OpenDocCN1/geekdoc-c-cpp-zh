
## 14
## De-Noising Raman Spectra Using Total Variation De-Noising with Iterative Clipping Algorithm

Padmesh Tripathi, Nitendra Kumar, and A. H. Siddiqi

## CONTENTS
- 14.1 Introduction............................................................................... 225
- 14.2 Material and Method....................................................................... 227
- 14.2.1 Material ................................................................................... 227
- 14.2.2 Total Variation (TV) De-Noising................................................... 227
- 14.2.3 Algorithm for TV De-Noising....................................................... 227
- 14.2.4 Numerical Implementation and Performance Analysis ................... 228
- 14.3 Results and Discussion .................................................................. 228
- 14.4 Conclusions................................................................................... 230
- References........................................................................................... 230

### 14.1 Introduction

Raman spectroscopy is a kind of molecular scattering spectroscopy that is characterized by frequency excursion that can be used to access information about the molecular structure of materials. It is a powerful non-destructive tool used in the estimation of chemical and physical properties of materials. It has a broad application in bio-medical, chemical, environmental, and industrial fields. The weak nature of Raman scattering results in the spectra with very low SNR can greatly influence the analytical results. There are three possible forms of noise in Raman spectra: high-frequency noise, which comes from the data acquisition electronic circuit and other sources of system variation; low-frequency noise, which arises from ambient light entering the spectrograph and fluorescence emission from the sample; and cosmic spikes, which are spurious and appear as very narrow spikes.

De-noising a signal is the process of removing the noise from the signal. Due to its applicability in many fields, it has been the center of attraction for engineers and scientists. Several techniques and methods have been used by researchers in recent years. Such a de-noising technique is based on total variation which was pioneered by Rudin et al. (1992). The generalization and extension of theories of total variation were done by Bredies et al. (2010), Hu and Jacob (2012), and Rodrigues and Wohlberg (2009). In regularization using total variation, minimization of a cost function is used to obtain the de-noising filter. All those algorithms that give a solution to the optimization problem of de-noising can be applied in the implementation of the total variation regularization. Many algorithms have been used to solve the problem. Selesnick and Bayram (2014) have developed an algorithm using the approach of Chambolle (2000), which has been used in this chapter. There are only a few reports on application of total variation for de-noising the Raman spectra. Liao et al. (2015) have used total variation to de-noise stimulated Raman spectroscopic images. Tripathi and Siddiqi (2016) have used total variation in de-noising Raman spectra solving an inverse problem.

The de-noising of Raman spectra is one of the important parts of spectral analysis. Two types of methods have been used for de-noising the Raman spectra: filtering and smoothing (Clupek et al., 2007). For filtering, the main methods used are: finite impulse response filtration, wavelet transform, and factor analysis. In finite impulse response (FIR) filtration, spectral shape is preserved, but it needs a lot of computations (Clupek et al., 2007). Wavelet transform has been established with the Fourier transform as a data-processing method in analytical fields. Several variants of wavelet transform (Ehrenreich and Summchen, 2001; Wang et al., 2006; Kumar et al., 2014; Maury and Revilla, 2015) have been used to de-noise the Raman spectra. In this method, spectral data is decomposed into the wavelet domain and reconstructed after thresholding for noise removal. In factor analysis (which is not applicable for filtering single spectrum), singular values play an important role. Singular values are the positive square roots of the eigenvalues. Using singular value decomposition, acquired spectra are projected into the orthonormal set of subspectra. Small singular values are taken as white noise. The role of large singular values is vital in maintaining the information of original spectra (Palacky et al., 2011). On the other hand, the classical Savitzky–Golay (SG) algorithm is very often used as the smoothing method to de-noise Raman spectra (Kwiatkowski et al., 2010). In this algorithm, the signal-to-noise ratio is increased without much distortion of the signal. Here, each segment of the original Raman spectrum in a small window is smoothed by fitting it to a low-degree polynomial using the least-squares. Besides these methods, Weiner estimation (Chen et al., 2013; Chen et al., 2014) has also been used for de-noising the Raman spectra.

Inverse problems deal with determining an input that produces an observed output, or determining an input that produces a desired output, often in the presence of noise. Mathematically, let A: X →Y be an operator that represents the association between the model parameter x and data y. Here X and Y are two spaces with appropriate structure. For a given input x, judging the outcome y is termed a direct problem. On the contrary, when given an observed outcome y, to judge an input x that produces it is termed an inverse problem. The solution minimizing

‖Ax − z‖₂² + λ‖Lx‖₁

is known as total variation regularized solution. Here, L is a smoothing operator that depends on application and λ is a parameter called a regularization parameter. Selection of λ plays an important role in solving an inverse problem (Wen and Chan, 2012; Langer, 2017).

In this chapter, Raman spectra of Zr doped BaTiO₃ (BZT) has been de-noised with the help of the total variation and the iterative clipping algorithm proposed by Selesnick and Bayram (2014). Two parameters—SNR and RMSE—are used to observe the performance of the algorithm. These are computed for different values of λ. The computed values of SNR and RMSE show that the iterative clipping algorithm with total variation is an effective algorithm to de-noise the Raman spectra.

### 14.2 Material and Method

In this chapter, the de-noising of Raman spectra of material Barium Zirconium Titanate is done using a method based on total variation.

#### 14.2.1 Material

FT-Raman spectra of Zr doped BaTiO₃ (BZT) with composition (x) = 0.010 has been carried out at room temperature. The spectra has been recorded in back scattering geometry by means of a Varian (Digilab), a dedicated FT-Raman Spectrometer (Nd-YAG Laser, 1064 nm, 500 mW laser power) in the range of 100 cm⁻¹–4000 cm⁻¹.

#### 14.2.2 Total Variation (TV) De-Noising

For a given M-point signal s(m) such that 0 ≤ m ≤ M−1, the total variation of s(m) is defined by:

$$TV(s)=\sum_{m=1}^{M-1}|s(m)-s(m-1)|=\|Ds\|_1$$

where D is a matrix of order M−1 × M.

For a given measured data y(m) containing noise and represented by

$$y(m)=s(m)+\varepsilon(m),\quad m=0,1,2,\ldots,M-1$$

where s(m) is a piecewise constant signal and ε(m) is white Gaussian noise, estimation of s(m) is the inverse problem. Estimate of the signal s(m) using TV de-noising is obtained by the solution of the optimization problem

$$\underset{s\in\mathbb{R}^{M}}{\operatorname{arg\,min}}\left\{J(s)=\frac{1}{2}\|y-s\|_2^2+\lambda\|Dx\|_1\right\}$$

It is worth noting here that the degree of smoothing is controlled by λ (Santamarina and Fratta, 2005).

#### 14.2.3 Algorithm for TV De-Noising

In Equation (14.2), replacing D by a matrix A of order M × N and using the min–max property (Rockafellar, 1970; Hiriart-Urruty and Lemarechal, 1993) and the majorization-minimization method (Figueiredo et al., 2007), Selesnick and Bayram (2014) have developed the iterative clipping algorithm as:

$$x^{(i+1)}=y-\frac{\lambda}{2}A^Tz^{(i)}$$

$$z^{(i+1)}=\operatorname{clip}\left(z^{(i)}+\frac{2}{\alpha\lambda}Ax^{(i+1)},1\right)$$

where i is the iteration index.

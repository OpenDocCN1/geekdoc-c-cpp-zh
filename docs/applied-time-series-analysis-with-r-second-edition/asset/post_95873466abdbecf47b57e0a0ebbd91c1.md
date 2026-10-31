
$$\int_{-\infty}^{\infty} \psi_{\ell,m}(t)\psi_{j,k}(t)\,dt = \begin{cases} 0, & j \neq \ell \text{ or } m \neq k \\ \|\psi\|^2, & j = \ell,\ m = k \end{cases}$$

Consequently,

$$d_{j,k} = \frac{1}{\|\psi\|^2}\int_{-\infty}^{\infty} g(t)\psi_{j,k}(t)\,dt.$$

## Appendix 12B: Mathematical Preliminaries

Many of the R functions used in this chapter are available in wavelet-based CRAN packages. However, three tswge functions were used: `wv.wge`, `plotts.dwt.wge`, and `plotts.mra.dwt`. These are discussed below, followed by a brief discussion of other packages.

- a. `wv.wge(x)` calculates and plots the Wigner–Ville time–frequency representation for the data in vector `x`.
  - `x` is a vector containing the realization to be analyzed.
  - *Example:* The Wigner–Ville plot shown in Figure 12.4b for the tswge data set `chirp` (shown in Figure 12.2a) is obtained using the following commands:

    ```
    data(chirp)
    wv.wge(chirp)
    ```

The following two commands are to be used in conjunction with the `dwt` and `mra` functions in the CRAN package `waveslim`.

- b. `plotts.dwt.wge(x, n.levels, type)`
  - This function calculates the dwt, outputs the wavelet coefficients, plots the DWT in the format of Figure 12.7, and optionally plots the scalogram (time-scale plot).
  - `x` is the realization to be analyzed (`x` must be a vector of length $2^{J_0}$ for some positive integer $J_0$ between 2 and 14).
  - `n.levels` (default = 4) is the number of levels ($n.levels \le J_0$).
  - `type` specifies the type of wavelet used (default = s8), i.e. the Symlet(8) wavelet.
  - Other choices are the Daublet wavelets D4 (shark fin), D6, and D8 and the Haar wavelet (`haar`).

  The program outputs:

  - `d1` through `d(n.levels)`, i.e. the `n.levels` sets of wavelet coefficients.
  - `s(n.levels)`, i.e. the scale coefficients associated with `n.levels`, along with information concerning wavelet type (e.g. `haar`, D4, etc.) along with the attributes `boundary` and `class`, which are by default set to `dwt` and `periodic`. For more information about these attributes, see the `waveslim` documentation.

  **NOTES:** `plotts.dwt.wge` plots a DWT based on the `waveslim` function `dwt` (see the `waveslim` documentation for more details).

  **Example:** To obtain the DWT shown in Figure 12.13a for the `bumps256` data set, use the following commands:

  ```
  data(bumps256)
  plotts.dwt.wge(bumps256, n.levels = 5, type = 'D6')
  ```

- c. `plotts.mra.wge(x, n.levels, type)`
  - `x` is the realization to be analyzed (`x` must be a vector of length $2^{J_0}$ for some positive integer $J_0$ between 2 and 14).
  - `n.levels` (default = 4) is the number of levels ($n.levels \le J_0$).
  - `type` specifies the type of wavelet used (default = S8), i.e. the Symlet(8) wavelet. Other choices are the Daublet wavelets D4 (shark fin), D6, and D8 and the Haar wavelet (`haar`).

  The program outputs:

  - `S0` through `S(n.levels)`, i.e. the approximations shown in Figure 12.9b, each of which has the same number of points as does `x`.

  **NOTES:** `plotts.mra.wge` plots an MRA based on the `waveslim` function `mra` (see the `waveslim` documentation for more details).

  **Example:** To obtain the MRA shown in Figure 12.9b for the `bumps256` data set, use the following commands:

  ```
  data(bumps256)
  plotts.mra.wge(bumps256, n.levels = 4, type = 'S8')
  ```

  In order to obtain the MRA plots in Figure 12.10a and b, replace the second command above with

  ```
  plotts.mra.wge(bumps256, n.levels = 4, type = 'haar')
  ```

  and

  ```
  plotts.mra.wge(bumps256, n.levels = 4, type = 'D4')
  ```

  respectively.

### Other Packages

The following is a brief list of other wavelet packages that may prove to be useful, some of which have been used in this chapter.

- 1. **waveslim:** In addition to the applications of the `dwt` and `mra` functions in `waveslim` mentioned above, the `waveslim` package was used in this chapter for the following:
  - a. *Smoothing:* The smoothing of the noisy bumps signal (called `nbump256` in the code below) at the top of the left panel in Figure 12.11 was accomplished using `waveslim` functions `dwt`, `universal.thresh`, and `idwt` as follows:

    ```
    data(nbump256)
    nbumps256.dwt <- dwt(nbump256)
    snbumps256.dwt <- universal.thresh(nbump256.dwt)
    snbumps256 <- idwt(snbumps256.dwt)
    ```

  - b. *Two-dimensional wavelets:* The `waveslim`-based code for plotting the `barbara` image and associated DWT in Figure 12.3 were obtained using the following:

    ```
    par(mfrow = c(2,2), mar = c(.3,2.5,.5,1))
    data(barbara)
    bbarbara <- barbara[256:1,256:1]
    gcol <- c(0,.1,.2,.3,.4,.5,.6,.7,.8,.9,1)
    image(1:dim(bbarbara)[1], 1:dim(bbarbara)[2], bbarbara, col = gray(gcol))
    bbarbara.dwt <- dwt.2d(bbarbara, 'haar', 3)
    plot.dwt.2d(bbarbara.dwt)
    ```

- 2. **Rwave:** The Gabor spectrum in Figure 12.4a for the linear chirp data (tswge file `chirp`) can be obtained using the Rwave command

  ```
  cgt(input = chirp, nvoice = 50, freqstep = .02, scale = 25, plot = TRUE)
  ```

  (See the Rwave documentation for a discussion of the input parameters.)

- 3. **wavethresh:** The `wavethresh` function `draw` can be used to plot mother and father wavelets. For example, the command

window

- iv. Plot the AR spectral estimator
- v. Plot the Gabor (use `cgt` in Rwave) and Wigner–Ville spectra

In each case, discuss the information in the plots with regard to whether or not there is an indication of stationarity, TVFs, etc. If the process appears to be stationary, describe the frequency behavior. If the process has TVFs, discuss the resulting effect on the plots.

## 12.2 Consider the following mother wavelet:

$$\psi(x) = x,\quad -1 \le x \le 1$$
$$= 0,\quad \text{elsewhere}$$

Find and plot the following dilations and translations, $\psi_{j,k}(x)$:

- a. $j = 2, k = 0$
- b. $j = 2, k = 3$
- c. $j = -1, k = 3$
- d. $j = -2, k = 3$

## 12.3 This problem involves the analysis of the following three data sets:

- 1. prob12.3a
- 2. prob12.3b
- 3. prob12.1c

For these data sets:

a. Plot the following related to the DWT:
- i. DWT
- ii. MRA
- iii. Time scale plot (scalogram)

For each of these plots, discuss the information that the plot conveys.

## 12.4 Consider the three data sets in Problem 12.3. For each of these data sets plot the Wigner–Ville spectrum and compare it with the three wavelet-based plots produced in Problem 12.3b. Compare the plots with regard to the time–frequency spectral information.

## 12.5 Using Equation 12.24 and the matrix M given in Equation 12.26, show that

a. $x_1 = -\frac{1}{\sqrt{2}}d_{1,1} - \frac{1}{2}d_{2,1} - \frac{1}{\sqrt{8}}d_{3,1} + \frac{1}{\sqrt{8}}s_{3,1}$.
b. Find a similar expression for $x_2$.

## 12.6 Analyze the following data sets using wavelet analysis and the Wigner–Ville plot. Describe any TVF behavior, abrupt changes, etc. that are identified by these analyses.

- a. bat (echolocation signal of a big brown bat)
- b. doppler (a Doppler signal)
- c. prob12.6c (simulated data set)

## 13 G-Stationary Processes

### 13.1 Generalized-Stationary Processes

In Chapter 12, we considered window-based methods for analyzing nonstationary processes with time-varying frequencies (TVF). These include short-term Fourier transforms (Gabor), along with Wigner–Ville and wavelet representations. In this chapter, we introduce an altogether different approach for analyzing TVF data in which we extend the definition of stationarity to the class of generalized-stationary (or G-stationary) processes. This approach allows us to transform the time index of many nonstationary processes to an index set upon which they are stationary.

The presentation here will be introductory in nature, and no effort will be made to cover this topic in detail. Our approach is to include sufficient information to give the reader a basic understanding of this methodology. Most of the developments in this area have only recently appeared in the literature, and these references are given here as a source of further details.

### Definition 13.1

Let $\{X(t) : t \in S\}$ be a stochastic process defined on $S \subset \mathbb{R}$, let $u = g(t)$ be a mapping onto a set $R_g \subset \mathbb{R}$, and let $g^{-1}$ denote a specified inverse. Then $X(t)$ is a G-stationary process if

- i. $E[X(t)] = \mu$. (13.1)
- ii. $\mathrm{Var}[X(t)] = \sigma^2 < \infty$.
- iii. $E[(X(t) - \mu)(X(g^{-1}(g(t) + g(\tau))) - \mu)] = R_X(\tau)$.

The usefulness of this definition may not be immediately apparent. In order to better understand its implications, suppose $g$ is a transformation of the time axis

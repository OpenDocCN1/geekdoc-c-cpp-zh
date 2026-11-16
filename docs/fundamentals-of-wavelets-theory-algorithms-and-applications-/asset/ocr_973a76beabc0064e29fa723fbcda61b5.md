always IIR. We will, however, prove in Chapter 7 that we can use \( G_0 \) and \( G_1 \) for both reconstruction and decomposition purposes. This is a consequence of the duality principle that we briefly mentioned in Chapter 5.

The commonly used cubic spline and the corresponding semiorthogonal wavelet with their duals and magnitude spectra are shown in Figures 6.2 and 6.3. See Chapter 10 for the expressions of commonly used semiorthogonal scaling functions and wavelets. Table 6.1 gives the coefficients \(\{g_1[m, k]\}\) for \( m = 2 \) through 6.

# TABLE 6.1: Coefficients \( u_{m,k} := 2^{m-1} (2m - 1)! g_1[m, k] \) for Semiorthogonal Wavelet (\( g_1[m, k] = (-1)^m g_1[m, 3m - 2 - k] \))

| k | \( u_{m,k} \) | k | \( u_{m,k} \) | k | \( u_{m,k} \) |
|---|---|---|---|---|---|
| \multicolumn{2}{c}{\( m = 2 \)} | \multicolumn{2}{c}{\( m = 5 \)} | \multicolumn{2}{c}{\( m = 6 \)} |
| 0 | 1 | 0 | 1 | 0 | 1 |
| 1 | -6 | 1 | -507 | 1 | -2,042 |
| 2 | 10 | 2 | 17,128 | 2 | 164,868 |
| 3 | -39 | 3 | -1,66,304 | 3 | -5,314,970 |
| 4 | -147 | 4 | 7,48,465 | 4 | 72,108,334 |
| 5 | -303 | 5 | -1,900,113 | 5 | -410,288,436 |
| | | 6 | 2,973,560 | 6 | 296,526,880 |
| \multicolumn{2}{c}{\( m = 3 \)} | | | 7 | -525,228,384 |
| 0 | 1 | | | 8 | 633,375,552 |
| 1 | -29 | | | | |
| 2 | 147 | | | | |
| 3 | -303 | | | | |
| 4 | -1 | | | | |
| 5 | 4 | | | | |
| \multicolumn{2}{c}{\( m = 4 \)} | | | | |
| 0 | 1 | | | | |
| 1 | -124 | | | | |
| 2 | 1,677 | | | | |
| 3 | -7,904 | | | | |
| 4 | 18,482 | | | | |
| 5 | -24,264 | | | | |

# FIGURE 6.2: Linear spline, dual linear spline, the corresponding wavelets, and their magnitude spectra.
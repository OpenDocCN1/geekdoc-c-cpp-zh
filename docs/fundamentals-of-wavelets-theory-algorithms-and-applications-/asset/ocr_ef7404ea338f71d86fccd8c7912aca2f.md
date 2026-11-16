roughly the same results as the wavelet approach, it fails to recognize the unknown bearing by missing one of the two faults. We conclude that the new feature extraction methods using DWT and WP are comparable if not superior to the FFT approach. The FFT lacks the time-domain information and thus misses some of the more localized faults.

The feature vector normalization and conditioning play a key role in the convergence of the neural network while training. Without the normalization, the network does not converge to the desired network error. Convergence of the network produces the biases and the weights necessary for the testing of the real data. Three hidden layers are used to improve the convergence. The results are collectively given in Table 9.1.

# TABLE 9.1: Overall Performance of the Network for F, E, and F and E Class Bearings

| Value (%) | FFT | CWT | DWT | WP |
|---|---|---|---|---|
| \multicolumn{5}{|c|}{F Class Bearings} |
| Correct decision | 96.06 | 95.70 | 92.37 | 92.87 |
| Misclassification | 1.67 | 1.69 | 4.56 | 2.49 |
| Miss | 2.26 | 2.61 | 3.07 | 4.64 |
| \multicolumn{5}{|c|}{E Class Bearings} |
| Correct decision | 95.96 | 94.16 | 87.50 | 95.76 |
| Misclassification | 1.28 | 2.55 | 7.05 | 2.50 |
| Miss | 2.76 | 3.50 | 5.45 | 3.74 |
| \multicolumn{5}{|c|}{F and E Class Bearings} |
| Correct decision | 95.18 | 94.22 | 87.61 | 92.41 |
| Misclassification | 0.93 | 2.35 | 8.88 | 3.19 |
| Miss | 3.89 | 3.42 | 3.51 | 4.40 |

# 9.6 TWO-DIMENSIONAL WAVELETS AND WAVELET PACKETS
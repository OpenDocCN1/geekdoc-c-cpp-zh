nonlinear operator and an inner product?” The amazing answer is “yes, under certain conditions that is true.” These conditions are known as Mercer’s conditions: Given a kernel function \( K(\mathbf{a}, \mathbf{b}) \) of two vector-valued arguments, if for any \( g(\mathbf{x}) \) that has finite energy,¹ then \( \int K(\mathbf{a}, \mathbf{b})g(\mathbf{a})g(\mathbf{b})d\mathbf{a}d\mathbf{b} \ge 0 \), and there exists a mapping \( \Phi \) and a decomposition of \( K \) of the form

```
\( K(\mathbf{a}, \mathbf{b}) = \psi_i(\mathbf{a})\psi_i(\mathbf{b}). \) (A.16)
```

In Eq. A.16, the subscript \( i \) denotes the \( i^{th} \) element of the vector-valued function \( \psi \). Thus, that expression represents an inner product. Notice that Mercer’s conditions simply state that if \( K \) satisfies these conditions, then \( K \) may be decomposed into an inner product of two instances of a function \( \psi \). They do not say what \( \psi \) is, nor do they say what the dimensionality of \( \psi \) is. But that’s OK. We do not have to know. In fact, the vector \( \psi \) may have infinite dimensionality. That’s still OK.

One kernel that is known to satisfy Mercer’s conditions and that is very popular in the SVM literature is the radial basis function

```
\( K(\mathbf{a}, \mathbf{b}) = \exp \left( - \frac{(\mathbf{a} - \mathbf{b})^T(\mathbf{a} - \mathbf{b})}{2\sigma^2} \right). \) (A.17)
```

In the literature, Support Vector Machines have been applied to problems such as face recognition [A.6], bird recognition [A.10], general object recognition [A.2] breast cancer detection [A.1], and many others. In comparative analyses in the literature, they have empirically been shown to outperform classical classification tools such as neural networks and nearest neighbor rules [A.5, A.8, A.9]. Interestingly, in a comparison with a classifier based on hyperspectral data, an SVM-based classifier using multispectral data (derived from the original hyperspectral data by filtering) performed better than classifiers based on the original data [A.4].

# Bibliography

+   [A.1] P. S. Bradley, U. M. Fayyad, and O. L. Mangasarian. Mathematical programming for data mining: Formulations and challenges. INFORMS Journal on Computing, 11(3), 1999.

+   [A.2] P. Felzenszwalb, R. Girshick, D. McAllester, and D. Ramanan. Object detection with discriminatively trained part based models. IEEE Trans Pattern Anal Mach Intell., 32(9), 2010.

+   [A.3] R. Fletcher. Practical Methods of Optimization. Wiley, 1987.

+   [A.4] B. Karacaali and W. Snyder. On-the-fly multispectral automatic target recognition. In Combat Identification Systems Conference, Jun 2002.

+   [A.5] D. Li, S. M. R. Azimi, and D. J. Dobeck. Comparison of different neural network classification paradigms for underwater target discrimination. In Proceedings of SPIE, Detection and Remediation Technologies for Mines and Minelike Targets V, volume 4038, pages 334–345, 2000.

+   [A.6] E. Osuna, R. Freund, and F. Girosi. Training support vector machines: an application to face detection. In Proceedings of CVPR’97, Jun 1997.

+   [A.7] V. Vapnik. The Nature of Statistical Learning Theory. Springer, 1995.

¹ \( \int g_2(\mathbf{y}) d\mathbf{y} \) is finite).
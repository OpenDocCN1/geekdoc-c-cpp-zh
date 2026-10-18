# 8.6.3.3  **Non-coherent Detection**

Let α be the probability that a transmitted ternary symbol was a 0 and was also received correctly as a 0. Similarly, let β (or, δ) be the probabilities that a transmitted symbol was a 1 (or 2) and the received symbol is also a 1 (or 2). Proceeding in the same way as in the case of TSS, the *frame-correct rate (FCR)* is given by:

$$FCR = \alpha^{nP_0} \times \beta^{nP_1} \times \delta^{nP_2}.$$  (8.63)

where $P_0$, $P_1$ and $P_2$ are the probabilities of occurrences of 0, 1 and 2, respectively, in the transmitted message. The average number of 0’s in the TFNS frame asymptotically (for large $m$) is 44% and those of all non-zero symbols, i.e., 1 and 2 taken together will be 56%. That is, $P_0 = 0.44$ and $P_1 + P_2 = 0.56$. From symmetry, $\beta = \delta$. Therefore, the probability that a frame in TFNS will be received correctly is given by:

$$FCR = \alpha^{0.44n} \times \beta^{0.56n}.$$  (8.64)

Hence, the FER for a TFNS frame is $FER_{tfns} = 1 - FCR$.

# 8.6.3.4  **Performance Evaluation**

Assume we transmit the original binary frame of $m$ bits using non-coherent BFSK and the BER of the non-coherent BFSK is $\rho$. The probability that the whole frame will be received correctly is given by $(1-\rho)^m$. Thus, the FER for BFSK will be $FER_{bfsk} = 1-(1-\rho)^m$. This may be approximated as $m\rho$, because $\rho$ is usually very small. For a given frame size $m$, one can compare $FER_{tfns}$ with $FER_{bfsk}(=m\rho)$. To know the performance of TFNS with respect to non-coherent BFSK we can compare $FER_{tfns}/m$ with $\rho$. To compute $FER_{tfns}/m$, we denote $s_A = 1$, i.e., signal power $=s_A^2/2=1/2$. This corresponds to a signal-to-noise ratio (SNR) $=1/2\sigma^2$. We used MATLAB to implement the computations to find the
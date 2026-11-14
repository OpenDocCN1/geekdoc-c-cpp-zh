z. In this case, the polynomial is a first-order polynomial (the highest exponent absolute value is 1) and this is the real reason the filter is named a first-order filter—it's the polynomial order of the transfer function.

# 5.8 The z Transform

The z substitution does a good job at simplifying the underlying polynomial behavior of $e^{j\omega_0}$ and it lets us use polynomial math to solve DSP problems. But, there is an interesting application of $z = e^{j\omega_0}$ that simplifies the design and analysis of digital filters. In the graph from Chapter 1 (Figure 5.19) you can see how the indexing of the samples determines their place in time. The future samples have positive indices and the past (delayed) samples have negative indices.

We've seen that $e^{j\omega_0}$ is the delay operator, so $e^{-j\omega_0}$ means one sample of delay, or one sample behind the current one. Likewise, $e^{-j\omega_02}$ would be two samples behind and $e^{+j\omega_04}$ indicates 4 samples ahead or in the future. That means that $e^{j\omega_0}$ could also be used as a book-keeping device since it can relate the position in time of something (a sample, for us).

The rules for implementing the z transform on a discrete signal or difference equation are easy and can often be done by inspection. The current sample x(n) or y(n) transforms into the signal X(z) or Y(z). Instead of thinking of the sample x(n) you think of the signal X(z), where X(z) is the whole signal—past, present, and future.

![](bbox=[0.18, 0.465, 0.82, 0.845])

Figure 5.19: Our book-keeping rules shown graphically.
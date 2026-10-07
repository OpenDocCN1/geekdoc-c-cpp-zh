# Chapter 10

# Algorithms 303

The algorithm to factor a large integer N can be viewed as a sequence of reductions (and everything shown here in italics will be defined in good time):

+   * FACTORING is reduced to finding a nontrivial square root of 1 modulo N.
* Finding such a root is reduced to computing the order of a random integer modulo N.
* The order of an integer is precisely the period of a particular periodic superposition.
* Finally, periods of superpositions can be found by the quantum FFT.

We begin with the last step.

# 10.3 The quantum Fourier transform

Recall the fast Fourier transform (FFT) from Chapter 2. It takes as input an M-dimensional, complex-valued vector $\alpha$ (where M is a power of 2, so $M=2^m$), and outputs an M-dimensional complex-valued vector $eta$:

![](bbox=[0.368, 0.403, 0.843, 0.542])

where $\omega$ is a complex Mth root of unity (the extra factor of $\sqrt{M}$ has the effect of ensuring that if $|alpha_i|^2$ add up to 1, then so do $|eta_i|^2$). The preceding equation suggests an $O(M^2)$ algorithm, the classical FFT is able to perform this much faster and has the profound effect of making digital signal processing practically feasible. We will now see that quantum computers can implement the FFT exponentially faster, in $O(\log M)$ time!

But wait, can any algorithm take time M, the length of the input? The point is that we can encode the input in a superposition of $m = \log M$ qubits: after all, this superposition consists of $2^m$ amplitude values. In the notation we introduced earlier, we wrote the superposition as $\alpha = \sum_{j=0}^{M-1} \alpha_j |j\rangle$ where $\alpha_j$ is the amplitude of the m-bit binary string corresponding to the number $j$ in the natural way. This brings us an important point: the $|j\rangle$ is just another way of writing a vector, where the index of each entry is written explicitly in the special bracket symbol.

Starting from this input superposition $|\alpha\rangle$, the quantum Fourier transform (QFT) manipulates it appropriately in $m=\log M$ stages. Each stage evolves so that it encodes the intermediate results at the same stage of the
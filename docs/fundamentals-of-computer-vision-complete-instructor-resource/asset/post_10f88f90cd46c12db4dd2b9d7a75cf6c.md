
## 6.7 Conclusion

In this chapter we have, among other things, presented three approaches to the same problem: edge-preserving smoothing. Our purpose was to use this as an opportunity to teach three different philosophies of solving problems in Computer Vision: (1) develop an ad hoc “good idea” into an effective algorithm, (2) pose the problem as the solution to a differential equation, or (3) pose the problem as a minimization. With proper choice of parameters, the three methods produce similar results. MAP was shown to perform better, but that is because MAP not only smooths the image; it also maintains fidelity to the original image. It is often easier to pose Computer Vision problems as solutions to optimization problems.

The strategy of bilateral filtering first appeared in the literature 1995 in a paper [6.1] by Aurich and Weule, but the term “bilateral filtering” did not appear until 1998 [6.26]. It has been used in applications such as noise removal [6.2, 6.3, 6.19], image motion analysis [6.27], and many others. The authors of this book used it in converting from the image representation in digital cameras to conventional color, a process called demosaicking [6.24].

Optimization methods are so pervasive in this chapter that the chapter title could almost be “image optimization.” We set up an objective function, a function of the measured image and the (unknown) true image and find the (unknown) true image that minimizes the objective function. Two terms were introduced: a noise term, which depends on the measurement; and a prior term, which depends only on the true image. The “true” image is then determined by finding the image that minimizes the objective function. A variety of minimization techniques could be used. In this chapter, we use gradient descent with annealing, but other, more sophisticated and faster techniques, such as conjugate gradient, could be used.

## 6.8 Assignments

- Assignment 6.1: Implement the VCD algorithm in section 6.4.4 on an image that your instructor selects. Experiment with various run times and parameter settings.

- Assignment 6.2: In Eq. 6.29, the quadratic variation is presented as a prior term. A very similar prior would be the Laplacian. What is the difference? That is, are there image features that would minimize the Laplacian and not minimize the quadratic variation? Vice-versa? Note that we said “the Laplacian” and not “the squared Laplacian.” Comment on this.

- Assignment 6.3: Which of the following expressions represents the Laplacian?
  - (a) \(\frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2}\) (c) \((\frac{\partial^2 f}{\partial x^2})^2 + (\frac{\partial^2 f}{\partial y^2})^2\) (e) \(\sqrt{(\frac{\partial^2 f}{\partial x^2})^2 + (\frac{\partial^2 f}{\partial y^2})^2}\)
  - (b) \(\frac{\partial f}{\partial x} + \frac{\partial f}{\partial y}\) (d) \((\frac{\partial f}{\partial x})^2 + (\frac{\partial f}{\partial y})^2\) (f) \(\sqrt{(\frac{\partial f}{\partial x})^2 + (\frac{\partial f}{\partial y})^2}\)

- Assignment 6.4: One form of the diffusion equation is written as \(df/dt = h_x \otimes (c(h_x \otimes f)) + h_y \otimes (c(h_y \otimes f))\) where \(h_x\) and \(h_y\) estimate the first derivatives in the \(x\) and \(y\) directions, respectively. This suggests that four kernels must be applied to compute this result. Simple algebra, however, suggests that this could be rewritten as \(df/dt = c(h_{xx} \otimes f + h_{yy} \otimes f)\), which requires application of only two kernels. Is this simplification of the algorithm correct? If not, explain why not, and under what conditions this would be true.

- Assignment 6.5: Consider the following image objective function

\(H(f) = \sum_i \left( \frac{f_i - g_i}{\sigma^2} \right)^2 - \sum_i \exp \left( - \frac{(h \otimes f)_i^2}{\tau^2} \right) = H_a(f, g) + H_p(f).\)

The pixels of \(f\) are lexicographically indexed by \(i\), and the kernel \(h\) is

| -1 | 2 | -1 |
|---|---|---|
| -2 | 4 | -2 |
| -1 | 2 | -1 |

Let \(G_p(f_i)\) denote the partial derivative of \(H_p\) with respect to pixel \(k\), i.e., \(G_p(f_i) = \frac{\partial}{\partial f_k} H_p(f)\). Write an expression for \(G_p(f_i)\). Use kernel notation.

- Assignment 6.6: Continuing Assignment 6.5, consider *only* the prior term. Write an equation that describes the change in image brightness at pixel \(k\) as one iteration of a simple gradient descent algorithm.

- Assignment 6.7: Continuing Assignment 6.6, extend this differential equation (assume the brightness varies only in the \(x\) direction) by substituting the form for \(G_p(f_i)\) that you derived. Is this a type of diffusion equation? Discuss. (Hint: replace the application of kernels with appropriate derivatives).

- Assignment 6.8: In a diffusion problem, you are asked to diffuse a VECTOR quantity as in Eq. 6.8, instead of the brightness that you did in your project. Replace the terms in the diffusion equation with the appropriate vector quantities, and write the new differential equation. (Hint, you may find the algebra easier if you denote the vector as \([a \ b]^T\)).

- Assignment 6.9: The time that the diffusion runs is somehow related to blur. This is why some people refer to diffusions of this type as “scale-space.” Discuss this use of terminology.

- Assignment 6.10: On page 109, a list of properties is given that a prior function should have. Determine if the inverted Gaussian has these properties.

- Assignment 6.11: In Eq. B.7 of Appendix B, there is a minus sign in front of the sum, but in the next equation, that minus sign is gone. Where did it go?

- Assignment 6.12: I had an image that needed to be blurred, so I ran fDoG on it to convolve with a Gaussian of \(\sigma = 2\), but that wasn’t enough blur. So I then ran the same function, with \(\sigma = 2\) again, and the results were exactly what I wanted. Could I have gotten the same result by just running the program once? If so, what value of \(\sigma\) should I have used?

- Assignment 6.13: Early in this chapter, an equation is given that relates two Gaussian blurs to a single blur. Suppose you have already blurred an image using convolution with a Gaussian with \(\sigma = 0.5\). It turns out you actually needed to blur the original image with a Gaussian with a \(\sigma\) of 2.0. You don't have access to the original image, so how much more blurring should you do to the one image you already have?

- Assignment 6.14: In Appendix B, Eq. B.3 illustrates the partial derivative of an expression involving a kernel, by expanding the kernel into a sum. Use this approach to prove that Eq. B.8 can be derived from Eq. B.7. Do your proof using a one-dimensional problem, and use a kernel that is \(3 \times 1\). (Denote the elements of the kernel as \(h_{-1}\), \(h_0\), and \(h_1\)).

## Bibliography

- [6.1] Non-linear Gaussian filters performing edge preserving diffusion. In *Proceedings of the DAGM Symposium*, 1995.

- [6.2] M. Aleksic, M. Smirnov, and S. Goma. Novel bilateral filter approach: Image noise reduction with sharpening. In *Proceedings of the Digital Photography II Conference*, volume 6069. SPIE, 2006.

- [6.3] E. Bennett and L. McMillan. Video enhancement using per-pixel virtual exposures. In *Proceedings of the ACM SIGGRAPH conference*, 2005.

- [6.4] J. Besag. Spatial interaction and the statistical analysis of lattice systems. *J. Royal Stat. Soc.*, 36, 1974.

- [6.5] J. Besag. On the statistical analysis of dirty pictures. *Journal of the Royal Statistical Society*, 48(3), 1986.

- [6.6] G. Bilbro and W. Snyder. Range image restoration using mean field annealing. In *Advances in Neural Network Information Processing Systems*. Morgan-Kaufmann, 1989.

- [6.7] G. Bilbro and W. Snyder. Mean field annealing, an application to image noise removal. *Journal of Neural Network Computing*, 1990.

- [6.8] G. Bilbro and W. Snyder. Optimization of functions with many minima. *IEEE Transactions on SMC*, 21(4), July/August 1991.

- [6.9] A. Buades, B. Coll, and J. M. Morel. A non-local algorithm for image denoising. In *CVPR*, 2005.

- [6.10] D. Geiger and F. Girosi. Parallel and deterministic algorithms for mrfs: Surface reconstruction and integration. *AI Memo*, (1114), 1989.

- [6.11] D. Geman and S. Geman. Stochastic relaxation, Gibbs distributions, and the Bayesian restoration of images. *IEEE Trans. Pattern Anal. and Machine Intell.*, 6(6), November 1984.

- [6.12] S. Grossberg. Neural dynamics of brightness perception: Features, boundaries, diffusion, and resonance. *Perception and Psychophysics*, 36(5), 1984.

- [6.13] J. Hadamard. *Lectures on the Cauchy Problem in Linear Partial Differential Equations*. Yale University Press, 1923.

- [6.14] J. Hammersley and P. Clifford. Markov field on finite graphs and lattices. Unpublished manuscript.

- [6.15] E. Hensel. *Inverse Theory and Applications for Engineers*. Prentice-Hall, 1991.

- [6.16] S. Kapoor, P. Mundkur, and U. Desai. Depth and image recovery using a MRF model. *IEEE Trans. Pattern Anal. and Machine Intell.*, 16(11), 1994.

- [6.17] R. Kashyap and R. Chellappa. Estimation and choice of neighbors in spatial-interaction model of images. *IEEE Trans. Information Theory*, IT-29, January 1983.

- [6.18] S. Li. On discontinuity-adaptive smoothness priors in computer vision. *IEEE Trans. Pattern Anal. and Machine Intell.*, 17(6), 1995.

- [6.19] C. Liu, W. Freeman, R. Szeliski, and S. Kang. Noise estimation from a single image. In *Proceedings of the Conference on IEEE Computer Vision and Pattern Recognition*, 2006.

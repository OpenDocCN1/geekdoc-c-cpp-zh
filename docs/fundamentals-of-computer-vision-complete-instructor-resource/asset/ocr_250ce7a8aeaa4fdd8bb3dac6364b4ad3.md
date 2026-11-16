In this section, we have shown one way to do edge-preserving smoothing by formulating a process, based on a PDE, which does what is desired. There are many variations on edge-sensitive diffusion. Another approach to the same problem is based on minimization of an objective function to obtain equal or better results, and that approach is described in the next section. Before reading it, go back and reread section 3.3 and recall that defining and solving an optimization problem can provide a powerful approach to many applications.

# 6.5 Edge-Preserving Smoothing Using Optimization

In this section we approach the problem of removing noise from an image by estimating what the image looked like before the noise was added. To do this, an objective function will be derived whose minimum will be found by gradient descent. Several forms for the objective function will be found that will enable the user to specify desired properties of the solution. Implementation of the algorithm presented in this section is enabled by material in Appendix B.

# 6.5.1 An Objective Function for Noise Removal

This problem will involve several variables:

+   - **f** The image before it was corrupted by noise. It is unknown. Estimation of this image is the problem we must solve. Though it is an image, we construct the lexicographic representation and think of the image as a vector. The elements of **f** are then denoted \(f_i\).
+   - **g** The image that we measured. This is corrupted by noise. Its elements are \(g_i\). \(P(\mathbf{g}|\mathbf{f})\) The conditional probability. Given the (unknown) image **f**, this is the probability that the image **g** will be generated as a result of adding random noise to **f**.
+   - **P(f)** The "prior" or *a priori* probability. This is the probability that \(P(\mathbf{f})\) exists. That is, the probability without having any other information, that the first element of **f** has brightness \(f_0\), the second element of **f** has brightness \(f_1\), etc. For example, we might know a *prior* that all the images with which we are concerned are almost always locally constant.
+   - **P(f|g)** The posterior probability, or *a posteriori* probability, i.e., the probability that the first element of **f** has value \(f_0\), ..., given the measurement, and we know the measurement. We want to find the particular **f** that maximizes this probability. Thus, we call these algorithms Maximum A Posteriori probability (MAP) algorithms.
+   - **P(g)** The prior probability for **g**. This depends only on **g**, and not on **f**, and **f** is what we are trying to find, so this term is of no use. Setting it to one gives a reasonable function to optimize, as shown in Eq. 6.11.

All the terms described above may be related by a single equation, Bayes rule:

```
\(P(\mathbf{f}|\mathbf{g}) = P(\mathbf{g}|\mathbf{f}) \frac{P(\mathbf{f})}{P(\mathbf{g})}.\) (6.11)
```
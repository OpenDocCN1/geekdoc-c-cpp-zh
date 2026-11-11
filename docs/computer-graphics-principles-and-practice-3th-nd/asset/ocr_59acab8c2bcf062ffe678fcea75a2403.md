a mirror surface, the answer is “the mirror direction”; for a diffuse surface, it’s “light coming from any direction could produce light in the eye-ray direction.” For others, the answer lies somewhere in between. We need, given the direction ωo, to be able to draw samples from S² in a way that’s proportional to ωi → fᵣ(ωi, ωo) (perhaps multiplied by a cosine factor).

+   - In methods like photon mapping, where we “push” light out from sources rather than “gathering it toward the eye,” we instead need to address the problem: “Given that some light arrived at this surface point P from direction ωi, it will be scattered in many directions. Randomly provide me an outgoing direction ωo where the probability of selecting ωo is proportional to fᵣ(ωi, ωo).”

Clearly these two problems are closely related.

The collecting of samples is done with a **sampling strategy**. What we’ve outlined above—“Give me a sample that’s proportional to something”—comes up both in the Metropolis algorithm and in importance sampling. Other sampling strategies can be used in other approaches to integration. Sometimes it’s important to be certain that you’ve got samples over a whole domain, rather than accidentally having them all cluster in one area; in such cases, stratified sampling, Poisson disk sampling, and other strategies can generate good results without introducing harmful artifacts.

Regardless of the sampling approach that we use, the values we compute are always random variables, and their properties, as estimators of the corresponding integrals, are how we can measure the performance of the various algorithms.

Before we proceed, here’s a brief review of what we learned about Monte Carlo integration (following Kellerman and Sźirmay-Kalos [KSKAC02]).

To compute the integral of a function f over some domain H, we represent it as an expected value of a random variable:

∫_H f(x) dx = ∫_H (f(x)/p(x)) p(x) dx    (31.71)
= **E**[ f(x)/p(x) ],    (31.72)

where p is a probability density on the domain H. To estimate the expected value, we draw N mutually uncorrelated samples according to p and average them, resulting in

∫ f(x) dx = **E**[ f(x)/p(x) ]    (31.73)
≈ (1/N) Σ_{i=1}^N f(X_i)/p(X_i),    (31.74)

where the standard deviation of this approximation is σ/√N; σ² being the variance of the random variable f(X)/p(X). By choosing p to be large where f is large and small where f is small, we reduce this variance. This is called **importance sampling**, with p being the importance function. (If the samples are correlated, the variance reduction is not nearly as rapid; we’ll return to this later.)

With this in mind, let’s begin with a general approach to approximating the series solution to the rendering equation.
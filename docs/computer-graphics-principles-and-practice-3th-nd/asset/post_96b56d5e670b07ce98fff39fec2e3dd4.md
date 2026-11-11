
possible light paths, or else take a great many samples to get a good estimate (i.e., a low-noise image).

What’s the difference between a path tracer and a conventional ray tracer? Well, the path-tracing result tends to be noisy, as we mentioned earlier: We’re making Monte Carlo estimates of the radiance at each point, and there’s variance in these estimates. A basic ray tracer that only computes recursive rays when there’s a mirror reflection uses a very low-variance estimate of the diffusely scattered indirect light: It estimates it as zero! That makes the basic ray-traced image darker than it should be, but uncluttered with noise. On the other hand, by taking more samples in the path tracer, we can reduce the noise a lot. For a small ray-casting budget (i.e., you can only afford to cast a certain number of rays in your scene), the simple ray-tracer result is wrong but nice looking; the path-traced result is generally “right on average,” but noisy. As the ray-casting budget increases, the ray-traced result does not really improve (except for deeper levels of reflection), while the path-traced result gets less and less noise, and correctly includes diffusely scattered indirect light.

Finally, we’ve treated “measurement” as part of the wrapper for a path tracer, but we could instead include it in the thing being computed, so rather than estimating \(L_e\), we could estimate \(L\) multiplied by the measurement function \(M\). When we do so, the thing we’re integrating, expanded out recursively, is a product of some number of scattering functions and cosines, an \(L_e\) at the end, and \(M\) at the beginning. (If we’re integrating with respect to area rather than solid angle, there will also be some change-of-variables factors.) There’s a symmetry in this formulation: We could swap the roles of \(M\) and \(L_e\), and imagine rendering a scene in which the eye was emitting light according to \(M\), and it was being measured at the light sources using \(L_e\) as the measurement function. The integral we’d write down for estimating light transport in this “swapped” scene would be exactly the same as in the original. This provides some theoretical justification for the “trace rays from the eye” approach rather than tracing photons from the lights, the way nature does it: The integrals we’re estimating are the same.

### 31.18.4 Multiple Importance Sampling

When we consider alternative ways to sample from the space of light paths, we may find one sampling strategy that is effective for one class of paths and another that works well for a different class. It’s difficult to know in advance which will be useful in any particular scene. Veach developed **multiple importance sampling** as a way to use many different sampling strategies in evaluating a single integral, by weighting samples from the different strategies differently. He describes a motivating example: a single glossy surface reflecting an area light source (e.g., think of a slightly rippled ocean reflecting moonlight). In this case, there are only two interesting kinds of paths: \(LE\) and \(LDE\); if the lights are outside the visible part of the scene, then there are only \(LDE\) paths. There are no paths of length greater than two in the scene. This makes the analysis particularly easy. We’ll look at only the \(LDE\) paths.

Suppose that we try to estimate the light arriving at some pixel, \(P\). One approach to sampling paths is that we trace a ray through \(P\), meeting the glossy surface at a point \(x\). Then we sample from the BRDF at \(x\) and trace a second ray that may hit the area light source, in which case the sample contributes some radiance, or that may miss the light altogether, in which case the sample contributes zero. An alternative approach is to trace the ray through \(P\) to \(x\), but then sample a point \(x'\) uniformly at random on the light source, and connect \(x\) to \(x'\). Now the path certainly carries some radiance.

![](img/f464cd0043eb5336aa0543fe20a0561b_919_0.png)

Figure 3.1.25: The image on the left was made by sampling the BRDF of the rough surface; the nearer slabs are rougher than the distant ones. Four light sources of varying sizes produce different glossy reflections. The image on the right used sampling on the light sources. The upper right in the first picture is preferable to that in the second; the lower left in the second picture is preferable to that in the first. No one sampling strategy is best. (Note that the scene is also lit by a weak light above the camera, and that the slabs all have a small diffuse component, letting us see their general shapes.) (Courtesy of Eric Veach.)

The second approach initially seems far better than the first approach, since the paths will always conduct some light. But what if the surface is very rough? Then the BRDF in the \(xx'\) direction may be nearly zero, and so the contribution is again very small. Figure 3.1.25 shows the results in practice.

Clearly we want to use one sampling strategy in estimating the integral in some cases, the other in other cases, and a mix of the two in still other cases. This is where multiple importance sampling comes in. Before we discuss that, there’s one point worth noting: If you have two estimators, one with large variance and one with small variance, and you average them, you’re in trouble: It’s really hard to get rid of the variance except by taking lots of samples. Informally speaking, the central idea of multiple importance sampling is that it provides a way to work with a kind of average of two estimators without letting the larger variance of one of them creep into the later computations.

To describe multiple importance sampling, we return to the abstract setting: We’re trying to integrate a function \(f\) on some domain \(D\), and we have two different sampling methods that produce samples \(X_{1,j}, j = 1, 2, \ldots\) and \(X_{2,j}, j = 1, 2, \ldots\), with density functions \(p_1\) and \(p_2\), respectively.

To estimate the integral using samples from the two different distributions, we need only produce two weighting functions, \(w_1\) and \(w_2\), from \(D\) to \(\mathbb{R}\), with two properties:

- \(w_1(x) + w_2(x) = 1\) for any \(x\) with \(f(x) \ne 0\).
- \(w_1(x) = 0\) whenever \(p_1(x) = 0\), and similarly for \(w_2\) and \(p_2\).

It generally makes sense for both weighting functions to be non-negative, in which case both vary between zero and one.

As a trivial example, at least in the case where each \(p_i\) is nonzero everywhere on the domain, we could pick \(w_1(x)=0.25\) for every \(x\), and \(w_2(x)=0.75\) for every \(x\). But more interesting cases arise when the weights are allowed to vary as a function of the samples. We’ll return to this in a moment.

Once we have chosen weighting functions, we take \(n_1\) samples of \(X_{1,j}\) from the first distribution, and \(n_2\) samples from the second, and combine them in the **multisample estimator** given by

\[
F = \frac{1}{n_1}\sum_{j=1}^{n_1} w_1(X_{1,j})\frac{f(X_{1,j})}{p_1(X_{1,j})} + \frac{1}{n_2}\sum_{j=1}^{n_2} w_2(X_{2,j})\frac{f(X_{2,j})}{p_2(X_{2,j})}. \tag{31.97}
\]

Veach shows that the multisample estimator \(F\) is in fact unbiased, and that with suitably chosen weights, it has good variance properties. (An exactly analogous formula works for three, four, or more samplers.)

What are good weight choices? The naive constant-weight approach is one; another is closely related: If we partition the domain \(D\) into two subsets \(D_1\) and \(D_2\) with \(D_1 \cup D_2 = D\) and \(D_1 \cap D_2 = \emptyset\), we can define \(w_i(x)=1\) when \(x \in D_i\), and \(0\) otherwise. This effectively says, “Use one kind of sampling on each part of the domain.” One application of this is when we partition the space of paths into, for instance, those with zero, one, two, … specular bounces, and use a different sampler for each. Another is when we’re sampling from a Phong-style BRDF and have to choose between a specular, a glossy, and a diffuse reflection.

### 31.18.5 Bidirectional Path Tracing

Path tracing makes its choice about extending paths based on the current point (i.e., `selectRay` is a function of only \(x_i\)). But the actual lighting in a scene may matter as well: If a bright light shines on a dark surface, considerable light may still be reflected. And lots of dim rays reflected even from a low-reflectance surface may converge to form caustics which are perceptually significant. In recognition of this, Lafortune and Willems [LW96] and Veach [VG94] independently proposed **bidirectional path tracing**, in which paths are traced both from light sources and from the eye. At a naive level, this sounds implausible: There’s essentially no chance that two such paths will ever land on the same point so that light is carried all the way from the luminaire to the eye! But a simple trick (see Figure 31.26) addresses this difficulty: We join the two paths with a segment! In fact, we can join any point on the first path to any point on the second path with such a segment, and compute the total transport along the resultant path.

![](img/f464cd0043eb5336aa0543fe20a0561b_920_0.png)

*Figure 31.26: A path is traced from the light and the eye; each point of the first path is connected to each point of the second to create paths from the luminaire to the eye. These connecting segments may, however, meet occluders (shown as black segments), creating no net transport.*

While the light-path and eye-path segments are all generated by tracing rays, and hence are guaranteed to transport light, the joining segments may meet occluders that make them transport no light at all. This potential occlusion can waste a great deal of path-tracing time and increase the variance of the pixel estimates. When the joining segment is *not* occluded, the computation of the contribution of the resultant path to the total transport is also very complex.

In practice, however, bidirectional path tracing tends to produce quite good results, good enough that they can (with enough samples) be used as a reference standard for evaluating other rendering methods.

To use the traced paths as samples for estimating the integral in the rendering equation, we need to know not only the transport along the path, but also the probability of having generated the path. Computing this probability requires careful

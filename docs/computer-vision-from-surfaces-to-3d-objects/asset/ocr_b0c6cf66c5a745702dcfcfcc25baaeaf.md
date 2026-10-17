the curvature of the surface in a manner that is defined by the perimeter to which the soap bubble clings. In principle, the shapes adopted by soap films on a wire frame are minimal surfaces. Note that if **H** = 0, then **κ₁** = −**κ₂** and the Gaussian curvature product is negative (or zero) throughout. Thus, minimal surfaces always have negative Gaussian curvature, meaning that they are locally saddle shaped with no rounded bulges or dimples of positive curvature. The surface tension principle operates to flatten any regions of net positive curvature until the mean curvature is zero.

Until 1967, it was thought that there were only two minimal surfaces exhibiting the property of **H** = 0, the negative-curvature hypersphere and the imaginary-curvature hyperboloid. Since that time, a large class of such surfaces has been discovered. These are very interesting surfaces with quasi-biological resonances, suggesting that the minimal surface principle is commonly adopted (or approximated) in biological systems (Figure 0.4). Thus, the simple specification of **H** = 0 generates a universe of interesting surface forms that may be of relevance in neural processing as much as they are in biological form. The ubiquitous operation of lateral inhibition at all levels in the nervous system is a minimal principle comparable with surface tension. It is generally viewed as operating on a 2D function of the neural array in some tissue such as the retina or visual cortex. However, for any form of neural connectivity that is effectively 3D, lateral inhibition may well operate to form minimal surfaces of neural connectivity with conforming mathematical minimal surface principle (or its dynamic manifestation).

A similar approach to this minimization for the 1D case over the domain Γ(x) has been proposed by Nitzberg, Mumford, and Shiota (1993) as minima of the elastic functional on the curvature **κ**:

```
$$E = \int_{\Gamma}(\nu + \alpha\kappa^2)\,dx,$$  (0.5)
```

where ν and α are constants.

Using a sparse set of depth cues Φ, one may define a function $f : \mathbb{R}^3 \to \mathbb{R}$ that estimates the signed geometric distance to the unknown surface S, and then use a contouring algorithm to extract the surface function approximating its zero set:

```
$$Z(f) = \{S(\Phi) \in \mathbb{R}^3 : S(\Phi) = 0\}$$  (0.6)
```

To make the problem computationally tractable (and a realistic model for neural representation within a 2D cortical sheet), we may propose a
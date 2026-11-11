```
~~~cpp
15  typedef std::vector<Impulse> ImpulseArray;
16
17  virtual ~BSDF() { }
18
19  /* Evaluates the finite portion of f(wi, wo) at a surface
20     whose normal is n. */
21  virtual Color3 evaluateFiniteScatteringDensity
22      (const Vector3&    wi,
23       const Vector3&    wo) const = 0;
24
25  ...
~~~
```

Listing 14.7 is an interface for the remaining methods needed for algorithms like photon mapping, recursive (Whitted) ray tracing, and path tracing. These are the methods for which the implementation and underlying mathematics are somewhat more complicated. We will not discuss them further here, except to note that the scattering methods are still straightforward to implement, given both the finite scattering density and the impulses, if we are willing to use rather inefficient implementations. There is nothing sacred about the particular methods we've included in this interface. In some implementations of path tracing, for instance, we want to sample with respect to a distribution proportional to the BSDF, without the extra weighting factor of ω_i · n, and we might include a method for that in our interface.

*Listing 14.7: An interface for a scattering function's scattering and impulse methods.*

```
~~~cpp
1  class BSDF {
2
3  ...
4
5  /* Given wi, returns all wo directions that yield impulses in
6     f(wi, wo). Overwrites the ImpulseArray. */
7  virtual void getOutgoingImpulses
8      (const Vector3&    wi,
9       ImpulseArray&    impulseArray) const = 0;
10
11
12 /* Given wi, samples wo from the normalized PDF of
13    wo -> g(wi, wo) * |wi . n|,
14    where the shape of g is ideally close to that of f. */
15 virtual Vector3 scatterOut
16     (const Vector3&    wi,
17      Color3&          weight) const = 0;
18
19
20 /* Given wi, returns the probability of scattering
21    (vs. absorption). By default, this is computed by sampling
22    since analytic forms do not exist for many scattering models. */
23 virtual Color3 probabilityOfScattering(
24     const Vector3& wi) const;
25
26 /* Given wo, returns all impulses for wi. */
27 virtual void getIncomingImpulses
28     (const Vector3&    wo,
29      ImpulseArray&    impulseArray) const = 0;
30
~~~
```
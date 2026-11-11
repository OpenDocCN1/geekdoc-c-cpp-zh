
If you are reading this indoors, then most of the light that you are seeing has been reflected multiple times. You can verify this by standing in an empty room with painted walls, illuminated by a single bulb. If you place a black occluder next to the bulb, some portion of the room will be “in shadow,” but nonetheless remains remarkably bright. The importance of this multiply reflected light is not well measured by computing energies, because of the logarithmic sensitivity of the eye: Even comparatively dark areas are easy for us to see; these darker areas are ones where indirect illumination has taken multiple attenuating bounces. Even though little energy from them is reaching the eye, we can easily detect variations on surfaces, such as the pattern on a carpet in a dark corner of a room.

These variations in dark regions can, however, be lost in the presence of other light. Figure 29.16 shows how the view through a car window can be masked by reflected light from papers on the dashboard.

Keep these examples in mind as you read about rendering algorithms, and ask yourself which of them each algorithm is capable of replicating.

## 29.9 Discussion

The key ideas in this chapter are the reflection equation and the transport equation, which combine to form the rendering equation, and the measurement equation, which is added as a final step in the process of image formation. Equally important is the notion of dividing various phenomena into “impulse” and “finite” pieces. This division applies to the BSDF, where impulses include mirror reflection and Snell’s-law refraction, and to luminaires, where point lights act as a kind of impulse in the illumination. Such impulses require that we regard integrals with a skeptical eye, because integrals of finite pieces can be reliably estimated with Monte Carlo methods, as we’ll see in the next few chapters, while those involving impulses must be treated separately.

The physical formulation of light transport is central to rendering, but it’s also worth understanding the *phenomena*, that is, the human-perceived aspects, of light transport. The tiny “rainbows” cast by a chandelier on the walls of a well-lit room are insignificant in the total illumination by physical measures, but to a person sitting in the room, they are important characteristics that attract attention. Understanding these phenomena helps us understand which aspects of physical light transport may have greater impacts on the perceived correctness of an image.

## 29.10 Exercise

- **Exercise 29.1:** Show that if you have the ray-casting function \(R\), then you can build a **visibility function** \(V : \mathcal{M} \times \mathcal{M} \to \{0, 1\}\), where \(V(P, Q)\) is 1 if all points of the line segment from \(P\) to \(Q\) that are strictly between the ends are in empty space, and is 0 otherwise. Informally, \(V(P, Q)\) is 1 when \(Q\) is visible from \(P\) (and vice versa). Note that according to our definition, \(V(P, P)\) is always 1. You may assume that you have a mechanism for perfect equality testing of points.

![](img/f464cd0043eb5336aa0543fe20a0561b_849_0.png)

*Figure 29.13: Under diffuse light, the catacaustic disappears.*

![](img/f464cd0043eb5336aa0543fe20a0561b_849_1.png)

*Figure 29.14: Distorted reflections.*

![](img/f464cd0043eb5336aa0543fe20a0561b_849_2.png)

*Figure 29.15: Refraction of light by water can break up spatial continuity.*

![](img/f464cd0043eb5336aa0543fe20a0561b_849_3.png)

*Figure 29.16: The reflections from the dashboard obscure the view through the window.*

## Chapter 30

## Probability and Monte Carlo Integration

### 30.1 Introduction

In preparation for studying rendering techniques, we now discuss Monte Carlo integration. We start with a rapid review of ideas from discrete probability theory, and then generalize to continua like the real line or the unit sphere. We apply these notions to describe how to generate random samples from various sets. We then introduce Monte Carlo integration, treating all the basic ideas through the integration of a function on an interval \([a,b]\), where the ideas are easiest to understand. We then show how these ideas apply to integration on a hemisphere or sphere, and hence how they are used to find reflected radiance via the reflectance equation, for instance.

### 30.2 Numerical Integration

We’ll start with a high-level overview of the use of randomization in numerical integration. Sometimes we need to integrate functions where computing antiderivatives is impossible or impractical. For instance, the integrand in the reflectance equation might not be described by an algebraic equation at all. In these cases, numerical methods often are the only workable solution. Numerical methods fall into two categories: deterministic and randomized. Here’s a quick comparison of the two.

A typical deterministic method (see Figure 30.1) for integrating a function \(f\) over an interval \([a,b]\) is to take \(n+1\) equally spaced points in the interval \([a,b]\), \(t_0=a, t_1=a+\frac{b-a}{n}, \ldots, t_n=b\), and evaluate \(f\) at the points \(t_{i+\frac{1}{2}}\) of each of the intervals these points define, sum up the results, and multiply by \(\frac{b-a}{n}\), the width of each interval. For sufficiently continuous functions \(f\), as \(n\) increases this sum will converge to the correct value. Similar methods for surface integrals, which divide

![](img/f464cd0043eb5336aa0543fe20a0561b_851_0.png)

the surface into small rectangles, also work. Press et al. [Pre95] describe these and more sophisticated deterministic methods.

A probabilistic or **Monte Carlo method** for computing, or more precisely, for *estimating* the integral of \(f\) over the interval \([a,b]\), is this: Let \(X_1,\ldots,X_n\) be randomly chosen points in the interval \([a,b]\). Then \(Y=(b-a)\frac{1}{n}\sum_{i=1}^{n}f(X_i)\) is a random value whose average (over many different choices of \(X_1,\ldots,X_n\)) is the integral \(\int_a^b f\). To implement this we use a random number generator to generate \(n\) points \(x_i\) in the interval \([a,b]\), evaluate \(f\) at each, average the results, and multiply by \(b-a\). This gives an estimate of the integral, as shown in Figure 30.2. Of course, each time we compute such an estimate we’ll get a different value. The variance in these values depends on the shape of the function \(f\). If we generate the random points \(x_i\) nonuniformly, we must slightly alter the formula. But in using a nonuniform distribution of points we gain an enormous advantage: By making our nonuniform distribution favor points \(x_i\) where \(f(x)\) is large, we can drastically reduce the variance of our estimate. This nonuniform sampling approach is called **importance sampling**. Figure 30.3 shows an example.

![](img/f464cd0043eb5336aa0543fe20a0561b_852_0.png)

*Figure 30.2: Estimating \(\int_{-1}^{1}\sqrt{1-x^2}\,dx\) with 20 samples approximates the correct result, which is \(\frac{\pi}{2} \approx 1.571\).*

We can integrate a function \(f\) over a surface region \(R\) by an analogous method. We choose points uniformly randomly on \(R\), average the values of \(f\) at these points, and multiply by the area of the region. Or we can generate points nonuniformly, and compute a weighted average, again multiplied by the region’s area, generalizing importance sampling. Our main application of numerical integration is when \(R\) is either the sphere or the outward-facing hemisphere at some surface point \(P\) where we’re trying to compute the scattered light (i.e., trying to evaluate the integral in the reflectance equation). We’ll return to this application at the end of the chapter.

![](img/f464cd0043eb5336aa0543fe20a0561b_852_1.png)

*Figure 30.3: Estimating the same integral, again with 20 samples, but preferentially selecting samples near \(x=0\), and using appropriate weighting, gives a better approximation.*

Randomized integration techniques form part of the working tools of anyone studying rendering, and much of the rest of graphics. Press et al. [Pre95] is a solid first reference for ideas beyond those discussed in this chapter.

### 30.3 Random Variables and Randomized Algorithms

Because the major shift in rendering methods over the past several decades was from deterministic to randomized, we’ll be discussing randomized approaches to solving the rendering equation. To do so means using random variables, expectation, and variance, all of which we assume you have encountered in some form in the past. To establish notation, and prepare for the continuum and mixed-probability cases, we review discrete probability here. The approach we take may seem a little unusual. That’s because our goal is not to *analyze* some probabilistic phenomenon that already exists (e.g., the chance of rainfall in Boston tomorrow, given that it’s already been raining for two days), but rather to *construct* probabilistic situations in which something computable, like expected value, turns out to have the same value as some integral (like the reflectance integral) that we care about. That leads to emphasis on some things that are largely downplayed in introductory probability courses.

We often find that for our students, the connection between formal probability theory and programs that implement probabilistic ideas is unclear, and so we discuss this connection as well.

Those familiar with these concepts can skip forward to Section 30.3.8.

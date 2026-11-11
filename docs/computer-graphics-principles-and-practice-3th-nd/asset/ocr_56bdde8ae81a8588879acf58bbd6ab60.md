If a point light hits a mirror surface or transmits through a translucent surface, we can then compute the result of its scattering from the *next* diffuse surface, etc. This eventually becomes a serious bookkeeping problem, and since point lights are merely a convenient fiction, we ignore it: We compute only diffuse scattering of point lights. Although addressing this properly in a ray-tracing-based renderer is difficult, we’ll see later that in the case of photon mapping, it’s quite simple.

One useful compromise for point-light sources is to say that for the purpose of emission directly toward the eye, the point source is actually a glowing sphere of some small radius, *r*, while when it’s used in the calculation of direct illumination, it’s treated as a point. This compromise, however, has the drawback that it requires the design of the class for representing lights to know something about the kinds of rays that will be interacting with it (i.e., an eye ray will be intersection-tested against a small sphere, while a secondary ray will never meet the light source at all), which violates encapsulation.

# ## 32.5 A Basic Path Tracer

Recall the basic idea of ray tracing and path tracing: For each pixel of the image, we shoot several rays from the eye through the pixel area. A typical ray (the red one in Figure 32.5) hits the scene somewhere, and we compute the direct light arriving there (the nearly vertical blue ray), and how it scatters back along the ray toward the eye (gray). We then trace one or more recursive rays (such as the yellow ray that hits the wall), and compute the radiance flowing back along them, and how it scatters back toward the eye, etc. Having computed the radiance back toward the eye along each of the rays through our pixel, we take some sort of weighted average and call that the pixel value.

Because of the usual description of ray tracing (“Start from the eye, and follow a ray out into the scene until it hits a surface at some point *P*, and ...”), we’ll use the convention that the rays we discuss are always the result of tracing *from the eye*, that is, the first ray points away from the eye, the second ray points away from the first intersection toward a light or another intersection, etc. (see Figure 32.6).

On the other hand, the radiance we want to compute is the radiance that flows along the ray in the other direction. If the eye ray *r* starts at the eye, *E*, and goes in direction ω, meeting the scene at a point *P*, then we want to compute *L*(*P*, −ω), that is, we want to compute the radiance in the *opposite* of *r*’s direction. We’ll have various procedures like `Radiance3 estimateTotalRadiance(Ray r, ...);` such functions always return the radiance flowing in the direction *opposite* that of *r*.

![](bbox=[0.714, 0.323, 0.957, 0.417])

![](bbox=[0.714, 0.473, 0.957, 0.611])

# ### 32.5.1 Preliminaries

We begin with a very simple path tracer, in which the image plane is divided into rectangular areas, each of which corresponds to a pixel. If a ray toward the eye passes through the (*i*,*j*)th rectangle, we treat the radiance as a sample of the radiance arriving at that rectangle. Despite the simplicity of the path tracer, we’ll use a lot of symbols, which we list in Table 32.1; we’ll define each one as we encounter it.
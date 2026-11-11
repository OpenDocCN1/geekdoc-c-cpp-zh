# Chapter 29

# Light Transport

# 29.1　Introduction

In this chapter we develop the **rendering equation**, which characterizes the light transport in a scene. We do this first for a scene in which there is no transmissive scattering, only reflection, and then generalize to handle transmission as well. In all but the simplest cases, the rendering equation is impossible to solve exactly. Approximation methods are therefore essential tools. The dominant approximation method involves estimating certain integrals by so-called Monte Carlo integration, that is, randomized integration algorithms, which we discuss in the next chapter. To assist with understanding the convergence properties of such algorithms, we can consider various kinds of light transport, some of which are amenable to study with one technique, some with another. For instance, a sequence of mirror reflections that conveys light from a point source to the eye must be treated rather differently from a sequence of diffuse reflections of illumination from an area light source. In fact, the phenomena produced by various kinds of light-transport paths can also be quite different at a perceptual level; we discuss this briefly, as well.

# 29.2　Light Transport

With the notion of the radiance field in hand, and that of the bidirectional reflectance distribution function (BRDF), we can now discuss light transport in general. We begin with the case of a scene consisting of empty space and purely reflective objects (i.e., there is nothing that’s partly transparent, and light reflects from the surfaces of objects—there’s no subsurface scattering to consider). The scattering of light from an object is therefore described by the BRDF, which we’ll denote \\(f_r\\) (the “r” standing for “reflection”). This special case conveys the main ideas but avoids some complexities. Having developed this first situation, we’ll generalize to other kinds of scattering, but with very few important changes.

We’ll continue with the assumptions of Chapter 26, that the scattering of light by a material comes in two parts: mirror and Snell-transmissive scattering, which
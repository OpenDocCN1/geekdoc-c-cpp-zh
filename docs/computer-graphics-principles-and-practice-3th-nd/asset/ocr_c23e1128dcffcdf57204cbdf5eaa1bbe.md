and reached the eye. Conventional regular-expression notation is useful here, with + used to indicate “one or more,” * for “zero or more,” ? for “zero or one,” parentheses for grouping, and | for “or,” so that L(D|S)E denotes a one-bounce path from a source to the eye that involves either a diffuse or specular reflection, while LD⁺E is a path involving one or more diffuse bounces.

**Inline Exercise 29.1.** (a) Write the notation for light that undergoes one or more diffuse bounces, and then a final specular bounce before reaching the eye. (b) A very basic ray tracer might consider rays from the eye that undergo only repeated specular bounces, followed by zero or one diffuse bounce, before reaching the light. Write the notation for the path traveled by the light, from luminaire to eye.

Note that the notation describes a sequence of scattering events, not just the path. In the case of the half-mirror surface we just discussed, light could travel from a luminaire to the surface, be mirror-reflected, and reach the eye; it could also travel from the source, be diffusely scattered, and reach the eye. The light energy in the two cases travels along the same path, but the first is described by LSE while the second is described by LDE.

There are extensions that are fairly common. Veach uses D to mean Lambertian, G for any kind of glossy reflection, S for perfectly specular, and T for transmission, for instance [Vea97].

We can use this notation to characterize certain rendering algorithms in terms of the eye paths that they consider, following Hanrahan [JAP⁺01]:

+   - Appel’s ray-casting algorithm: E(D|G)L
+   - Recursive ray tracing (Whitted): E[S*](D|G)L
+   - Path tracing (Kajiya): E[(D|G|S)⁺)D|G]L
+   - Radiosity: ED*L

Recursive ray tracing considers only light that’s diffusely or glossily reflected, and then mirror-reflected to the eye. Radiosity only handles diffuse reflections. And Appel’s ray-casting algorithm considers only direct lighting.

![](bbox=[0.707, 0.398, 0.934, 0.552])

![](bbox=[0.707, 0.576, 0.934, 0.729])

# 29.8.1 Perceptually Significant Phenomena and Light Transport

We conclude this largely mathematical chapter with a discussion of things we notice when we look at the world, for these phenomena—the things we take the trouble to name—are the things we must render effectively if we want to make compelling images. They thus serve as a guide to developing rendering algorithms.

The first phenomenon is the **shadow**. Figure 29.6 shows a hard shadow, created by a luminaire (the sun) that subtends a very small solid angle. The light from the sun is obstructed by the sharp edge of an object. Figure 29.7 shows a soft shadow. Soft shadows can be caused by many things: If the shadowing object is not sharply defined (e.g., a furry animal), the shadow may have no distinct edge, even if it’s cast by a point luminaire. If the shadow is cast by a very small object, diffraction effects may dominate and effectively soften the shadow. But most often, soft shadowing is caused by nonpoint luminaires: A point on the receiving surface may be

![](bbox=[0.707, 0.757, 0.934, 0.923])
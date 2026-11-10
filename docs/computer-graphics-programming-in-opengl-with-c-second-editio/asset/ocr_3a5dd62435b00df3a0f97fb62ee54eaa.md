of doing this would be to use the tessellation stage to increase the number of vertices, and then use height mapping to move them according to the values in the noise map.

Our simulation of the visible distortions on the floor have a fundamental inaccuracy, in that they are based on the noise values for the surface locations directly above the corresponding floor locations. Actually, the distortion for a given floor location should be based on the noise value for the surface location in between the camera and the floor location. However, it is unlikely to make a difference in the perceived realism. There are many simplifications such as this throughout our implementation.

“Fresnel” is pronounced “Fre-nel”—the “s” is silent.

There are numerous papers and resources for readers interested in diving more deeply into the topic of simulating water and other fluids. There are even entire books on the topic [315].

The technique described in this chapter was patterned closely after an implementation by Chris Swenson as part of a special project when he was a student at California State University, Sacramento. His contributions greatly facilitated our explanations and we appreciate the excellent work that he did generating a nicely coherent step-by-step approach.

# ## Exercises

+   - 15.1 Add a flying object such as a bird or airplane (or even the NASA space shuttle model) flying overhead, above the top surface of the water. Then include it in the reflection off the top surface of the water when the camera is above the water’s surface and in the refraction through the top surface when the camera is below the water surface.
+   - 15.2 Add an object moving underwater, such as a fish or submarine (or even the Studio 522 dolphin) below the top surface of the water. Then include it in the scene when the camera is below the top surface and in the refraction when the camera is above the top surface.
+   - 15.3 In exercise 15.2 (above), if you haven’t done so already, add water caustics to the underwater object.
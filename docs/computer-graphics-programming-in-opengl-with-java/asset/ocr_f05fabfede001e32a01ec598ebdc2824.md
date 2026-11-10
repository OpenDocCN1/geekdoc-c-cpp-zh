the camera and the floor location. However, it is unlikely to make a difference in the perceived realism. There are many simplifications such as this throughout our implementation.

“Fresnel” is pronounced “Fre-nel” — the “s” is silent.

There are numerous papers and resources for readers interested in diving more deeply into the topic of simulating water and other fluids. There are even entire books on the topic [B15].

The technique described in this chapter was patterned closely after an implementation by Chris Swenson as part of a special project when he was a student at California State University, Sacramento. His contributions greatly facilitated our explanations and we appreciate the excellent work that he did generating a nicely coherent step-by-step approach.

# Exercises

+   15.1 Add a flying object such as a bird or airplane (or even the NASA space shuttle model) flying overhead, above the top surface of the water. Then include it in the reflection off the top surface of the water when the camera is above the water’s surface and in the refraction through the top surface when the camera is below the water surface.
+   
+   15.2 Add an object moving underwater, such as a fish or submarine (or even the Studio 522 dolphin) below the top surface of the water. Then include it in the scene when the camera is below the top surface and in the refraction when the camera is above the top surface.
+   
+   15.3 In Exercise 15.2 (above), if you haven’t done so already, add water caustics to the underwater object.
+   
+   15.4 Modify the fragment shader in Program 15.8 so that the water caustics are also rendered when the camera is *above* the top surface as well. Do you think that the scene appears more realistic or less realistic with the caustics included in this case? If the latter, try to find a way to tune the caustics so that they increase realism rather than detracting from it.
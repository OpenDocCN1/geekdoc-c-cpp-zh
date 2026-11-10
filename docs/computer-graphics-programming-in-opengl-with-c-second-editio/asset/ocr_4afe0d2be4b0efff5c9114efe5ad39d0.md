**9.2** Draw labels on the six cube map image files to confirm that the correct orientation is being achieved. For example, you could draw axis labels on the images, such as these:

![](bbox=[0.149, 0.199, 0.851, 0.287])

Also use your “labeled” cube map to verify that the reflections in the environment-mapped torus are being rendered correctly.

**9.3** *(PROJECT)* Modify Program 9.3 so that the object in the scene blends environment-mapping with a texture. Use a weighted sum in the fragment shader, as described in Chapter 7.

**9.4** *(RESEARCH & PROJECT)* Learn the basics of how to use Terragen [TE19] to create a simple cube map. This generally entails making a “world” with the desired terrain and atmospheric patterns (in Terragen), and then positioning Terragen’s synthetic camera to save six images representing the views front, back, right, left, top, and bottom. Use your images in Programs 9.2 and 9.3 to see their appearance as cube maps and with environment mapping. The free version of Terragen is quite sufficient for this exercise.

# References

**[BO11]** P. Bourke, “Representing Star Fields,” October 2011, accessed July 2020, http://paulbourke.net/miscellaneous/astronomy/

**[dV14]** J. de Vries, “Learn OpenGL — Cubemaps,” 2014, accessed July 2020, https://learnopengl.com/Advanced-OpenGL/Cubemaps

**[GE16]** A. Gerdelan, “Cube Maps: Sky Boxes and Environment Mapping,” 2016, accessed July 2020, http://antongerdelan.net/opengl/cubemaps.html

**[GI20]** GNU Image Manipulation Program, accessed July 2020, http://www.gimp.org
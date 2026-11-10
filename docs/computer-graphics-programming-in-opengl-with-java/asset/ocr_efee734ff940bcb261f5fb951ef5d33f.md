This is an example of a *culling* technique, and it is a very useful one because of the load that instanced tessellation can still place on the system.

The four-parameter version of createShaderProgram() used in Program 12.1 is added to the Utils.java file. Later, we will add additional versions to accommodate the geometry shader stage.

# Exercises

+   12.1 Modify Program 12.1 to experiment with various values for inner and outer tessellation levels and observing the resulting rendered mesh.
+   
+   12.2 Test Program 12.5 with the layout specifier in the evaluation shader set to equal_spacing, and then to fractional_even_spacing, as described in Section 12.4. Observe the effects on the rendered surface as the camera moves. You should be able to observe popping artifacts in the first case, which are mostly alleviated in the second case.
+   
+   12.3 *(PROJECT)* Modify Program 12.4 to utilize a height map of your own design (you could use the one you built previously in Exercise 10.2). Then add lighting and shadow mapping so that your tessellated terrain casts shadows. This is a complex exercise, because some of the code in the first and second shadow mapping passes will need to be moved to the evaluation shader.

# References

[GN12] GIMP normal map plugin, accessed March 2021, https://code.google.com/archive/p/gimp-normalmap/

[HT12] J. Hastings-Trew, *JHT’s Planetary Pixel Emporium*, accessed March 2021, http://planetpixelemporium.com/

[LU16] F. Luna, *Introduction to 3D Game Programming with DirectX 12*, 2nd ed. (Mercury Learning, 2016).
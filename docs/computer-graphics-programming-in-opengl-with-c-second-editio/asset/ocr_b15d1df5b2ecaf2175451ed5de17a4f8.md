![](bbox=[0.22, 0.1, 0.79, 0.56])

Figure 16.3
Output of Program 16.2, showing simple ray casting without lighting

# ### 16.2.6 Adding ADS Lighting

ADS (“ambient-diffuse-specular”) lighting was covered in Chapter 7. Here we implement it in the ray casting compute shader by adding code that specifies the global ambient light, the position and ADS characteristics of a positional light, ADS material characteristics of the objects in the scene, and a function to compute the ADS lighting in the same manner as was done in Chapter 7.

Program 16.3 shows the additions and changes to the ray casting compute shader. There are declarations added at the top of the shader, and a new function ads_phong_lighting(). Changes to the raytrace() function are shown in red, in which the lighting result is multiplied by the color of the object. In this simple example,
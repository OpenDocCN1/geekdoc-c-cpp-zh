Computing the world coordinates of the nearest collision is then done the same as for the sphere. Computing the normal at this point is then either (±1,0,0), (0,±1,0) or (0,0,±1), depending on which surface the collision occurs.

# 16.2.5 Output of Simple Ray Casting Without Lighting

Figure 16.3 shows the output of Program 16.2. The scene contains a red sphere on the right, and a green box on the left. The box is axis-aligned, and is placed slightly closer to the camera than the sphere. Note that lighting has not been applied, so the surfaces appear flat and the sphere just looks like a disk.

![](bbox=[0.313, 0.354, 0.686, 0.666])

**Figure 16.3**  
Output of Program 16.2, showing simple ray casting without lighting.

# 16.2.6 Adding ADS Lighting

ADS (“ambient-diffuse-specular”) lighting was covered in Chapter 7. Here we implement it in the ray casting compute shader by adding code that specifies the global ambient light, the position and ADS characteristics of a positional light, ADS material characteristics of the objects in the scene, and a function to compute the ADS lighting in the same manner as was done in Chapter 7.
# Exercises

1. Consider a gray world with no ambient and specular lighting (only diffuse lighting). The light is at infinity and its direction and color are (1,1,1) and 1.0 respectively. The coefficient of diffuse reflection is 1/2. The normals at points P1, P2 and P3, are N1 = (0,0,1), N2 = (1,0,0) and N3 = (0,1,0) respectively. Find the illumination at the points P1, P2 and P3.

![](bbox=[0.26, 0.34, 0.73, 0.51])

2. In the above figure, the light and the eye are denoted by L and E respectively. On the surface AC the normals at A and C are NA = (-1,1,0) and NC = (1,1,0) respectively. Everything is drawn to scale. Use the illumination model given by I = Ia ka + IL kd (N.L) + IL ks (R.V)n where R denotes the reflected light vector at the surface point, Ia = 0.8, IL = 1.0, ka = 0.2, kd = 0.9, ks = 0.5, n = 2. Find the illumination at A and B. (Hint: Treat negative dot products as 0.)

3. You are rendering a black and white checkered tiled floor using a single texture mapped polygon. The view is simulating a person standing on the floor and looking at a point far away from him on the floor. (1)Artifacts at the distant end of the floor can be seen. How would you remove these artifacts? (2) How can you explain why this method works using the sampling theorem?

4. One artifact of Gouraud shading is that it can miss specular highlights in the interior of the triangles. How can this be explained as an aliasing artifact?

5. Consider five objects in the line of sight from the eye. Object i is behind Object i−1. Object 1, 3 and 5 are opaque while the others are translucent. In what order would you render the objects to get the correct effect of translucency? Justify your answer.

6. Consider the above 2D gray world and the primitive AB in it (shown by the red line). The blue vectors show the normal at A and B. L and E are the
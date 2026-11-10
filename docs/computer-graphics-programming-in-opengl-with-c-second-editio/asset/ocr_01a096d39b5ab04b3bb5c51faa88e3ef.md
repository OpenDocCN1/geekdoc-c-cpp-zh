Lighting models are sometimes called *shading models*, although in the presence of shader programming, that can be a bit confusing. Sometimes the term *reflection model* is used, complicating the terminology further. We will try to stick to whichever terminology is simple and most practical.

The most common lighting models today are called “ADS” models, because they are based on three types of reflection labeled A, D, and S:

+   - **Ambient reflection** simulates a low-level illumination that equally affects everything in the scene.
+   - **Diffuse reflection** brightens objects to various degrees depending on the light’s angle of incidence.
+   - **Specular reflection** conveys the shininess of an object by strategically placing a highlight of appropriate size on the object’s surface where light is reflected most directly toward our eyes.

ADS models can be used to simulate different lighting effects and a variety of materials.

![](bbox=[0.14, 0.465, 0.509, 0.646])

**Figure 7.1**
ADS lighting contributions.

Figure 7.1 illustrates the ambient, diffuse, and specular contributions of a positional light on a shiny gold torus.

Recall that a scene is ultimately drawn by having the fragment shader output a color for each pixel on the screen. Using an ADS lighting model requires specifying contributions due to lighting on a pixel’s RGBA output value. Factors include:

+   - The type of light source and its ambient, diffuse, and specular characteristics
+   - The object’s material’s ambient, diffuse, and specular characteristics
+   - The object’s material’s specified “shininess”
+   - The angle at which the light hits the object
+   - The angle from which the scene is being viewed
# MATERIALS

As previous sections have explained, the effect color given to a triangle in a scene depends on the light and the angle at which the light hits the triangle. The result also depends on the triangle's type of material. WPF provides three kinds of materials: diffuse, specular, and emissive.

A diffuse material's brightness depends on the angle at which light hits it, but the brightness does not depend on the angle at which you view it.

For example, hold a white sheet of paper so that it is perpendicular to the brightest light source near. If the light is bright, then when you move your head to look at the paper from different angles, it should appear roughly the same color (unless it's shiny paper, in which case it acts as a specular material—more than that of all). All the examples so far in this chapter have used diffuse materials.

A specular material is somewhat shiny. In that case, an object's brightness depends on how closely the angle between you, and the light sources match the object's mirror angle. The mirror angle is the angle at which most of the light would bounce off the object if it were perfectly shiny.

For example, suppose you have a perfectly shiny steel ball. If you looked closely, you would see a small image of the light reflected in the ball. The place where the reflection is the light's mirror angle points directly at you. On other parts of the ball, you will be off the mirror angle so you won't see the light's reflection.

If the ball is somewhat shiny, for example a billiard ball, then you'll see a bright patch where the mirror angle lines up. Areas near the mirror will slightly less bright and areas far from the mirror angle will be the least bright.

The final type of material, an emissive material, glows. An emissive material glows only on itself. In other words, it makes its own brightness, but it doesn't contribute to the brightness of other objects as a light would.

Specular and emissive materials are not really intended to be used alone. Most them are combined with a diffuse material in a MaterialGroup.

The example program shown in Figure 23-9 shows four spheres made of different materials. From left to right, the are diffuse, specular, emissive, and a MaterialGroup combining three types of materials.

Notice that the specular material adds a bright spot to the final and the emissive material makes the sphere brighter overall.

![](bbox=[0.545, 0.625, 0.905, 0.735])

FIGURE 23-9

```
The following code shows how the program creates its spheres:
MakeSingleSphere(Sphere0, new DiffuseMaterial(Brushes.Green), 1, 20, 30);
MakeSingleSphere(Sphere01, new SpecularMaterial(Brushes.Green), 50, 1, 30, 30);
MakeSingleSphere(Sphere02, new EmissiveMaterial(Brushes.DarkGreen), 1, 20, 90);
MaterialGroup combined_material = new MaterialGroup();
combined_material.Children.Add(new DiffuseMaterial(Brushes.Green));
```
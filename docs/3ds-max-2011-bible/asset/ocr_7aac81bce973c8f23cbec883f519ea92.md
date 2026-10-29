# Noise modifier

The Noise modifier randomly varies the position of object vertices in the direction of the selected axes. Noise parameters include Seed and Scale values, a Fractal option with Roughness and Iterations settings, Strength about each axis, and Animation settings.

The Seed value sets the randomness of the noise. If two identical objects have the same settings and the same Seed value, they look exactly the same even though a random noise has been applied to them. If you alter the Seed value for one of them, then they will look dramatically different.

The Scale value determines the size of the position changes, so larger Scale values result in a smoother, less rough shape. The Fractal option enables fractal iterations, which result in more jagged surfaces. If Fractal is enabled, Roughness and Iterations become active. The Roughness value sets the amount of variation, and the Iterations value defines the number of times to complete the fractal computations. More iterations yield a wilder or chaotic surface but require more computation time.

If the Animate Noise option is selected, the vertices positions will modulate for the duration of the frames. The Frequency value determines how quickly the object's noise changes, and the Phase setting determines where the noise wave starts and ends.

Figure 11.13 shows the Noise modifier applied to several sphere objects. These spheres make the Noise modifier easier to see than on the hammer object. The left sphere has Seed, Scale, and Strength values along all three axes set to 1.0, the middle sphere has increased the Strength values to 2.0, and the right sphere has the Fractal option enabled with a Roughness value of 1.0 and an Iterations value of 6.0.

# Cross-Ref

> The Physique modifier is one of the original Character Studio tools. Although both modifiers still exist, the Skin modifier is preferred. It is covered in Chapter 40, “Skinning Characters.”
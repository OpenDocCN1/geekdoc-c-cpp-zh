textures, such as for building shadows, generating water effects, or doing ray tracing. In those cases, the Java code would need to be further modified to manage the buffers. This is especially tricky in the water examples from Chapter 15, where the reflection and refraction buffers are largely estimated and won’t lend themselves to accurate splitting between the two eyes without modification.

We chose the fog example for rendering because the fog further helps the stereoscopic effect and because that example was not overly hampered by the color limitations of red/cyan anaglyph viewing. The colors of some of the other examples in the textbook will not fare as well when viewed in red/cyan anaglyph.

The reader no doubt has noticed that our side-by-side rendering was horizontally squished. We didn’t correct for this to keep the code as simple as possible. A more complete solution would also correct the view frustums so that the aspect ratio isn’t so radically changed. One drawback of side-by-side viewing is the resulting loss of half of the screen real estate when rendering a scene.

Details on the *vertex displacement* method for correcting lens distortion, which has better performance than the simple fragment-shader-based method presented in this chapter, can be found elsewhere [K16].

Although we have presented basic approaches to stereoscopic rendering (and viewing) such as are applied for virtual reality systems, there is quite a large set of VR topics that we haven’t discussed at all. A full VR system not only displays in stereoscopic 3D, it also includes sensors that enable the user to move and interact more naturally, such as by turning one’s head or reaching with the hands. We have focused solely on the graphics.

This chapter also doesn’t cover how to render for polarized or shutter technologies (although they are mentioned briefly in the beginning of the chapter). Those require more specialized hardware and their solutions are beyond the scope of this introduction.

# Exercises

+   17.1 Modify Program 17.1 to try a variety of different values for the IOD. What range of values do you think works the best for this scene? What happens if the IOD is set too small? What do you observe as the IOD increases, and then what happens when the IOD is set too large?
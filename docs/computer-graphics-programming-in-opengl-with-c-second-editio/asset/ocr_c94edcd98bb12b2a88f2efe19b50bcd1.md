```
```
float dist = length(varyingVertPos.xyz);
float fogFactor = clamp((fogEnd-dist) / (fogEnd-fogStart), 0.0, 1.0);
...
if (isAbove == 1) color = mix(fogColor, color, pow(fogFactor,5.0));
}
```
```

![](bbox=[0.144, 0.24, 0.854, 0.524])

**Figure 15.8**
Fresnel effect (left, above the water's surface) and fog effect (right, below the water's surface)

# ## 15.5 ANIMATING THE WATER MOVEMENT

Animating the water’s surface can be done in a similar manner as was done for clouds by taking advantage of the third dimension in the noise map (as yet unused). Recall from Section 14.8 the trick of replacing the texture lookup constant in the third dimension with a variable that changes over time. As the retrieved “slice” of the noise map changes, the noise details change. We can use that same trick here to move the sine wave by adjusting the position along the third axis over time when we look up which “slice” of the noise map to apply.

This modification is given in Program 15.7. Although we cannot adequately show the animation here, some frames showing the changes to the surface and lighting over time are given in Figure 15.9, viewed from both above and below the water’s surface. (Or, to see the actual movement, run the code on the accompanying files.)
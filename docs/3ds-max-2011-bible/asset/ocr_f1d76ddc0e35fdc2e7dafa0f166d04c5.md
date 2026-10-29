# Part XI: Advanced Lighting and Rendering

As an example of how this material can be used, consider the hot plate example. Rather than excluding objects from the Advanced Lighting calculations, you can instead use the Light Tracer panel to set the global settings for the scene and apply the Advanced Lighting Override material to the hot plate coils with a higher Color Bleed value. This causes the coils to bleed, but not the rest of the scene.

Another common use for this material is to use the Luminance Scale value to cause self-illuminating materials to add light energy to the global illumination calculations. In other words, increasing this value makes self-illuminating materials act as lights to the scene.

The Advanced Lighting Override material parameters, shown in Figure 45.15, let you set the amount of Reflectance, Color Bleed, Transmittance, Luminance, and Indirect Light Bump Scale that the material uses.

# FIGURE 45.15

The Advanced Lighting Override Material rollout defines how light interacts with the material.

![](bbox=[0.07, 0.52, 0.35, 0.75])

# Lightscape material

The Lightscape material type lets you apply a material to objects that are imported from Lightscape. They are used to control how the radiosity is mapped to objects. The Basic Parameters rollout includes values for Brightness, Contrast, Ambient Light, and Bump Amount. You also can enable Daylight and Exterior Scene options. These values are applied in addition to the base material.

# Using Lighting Analysis

To get information about the current lighting solution, you can use the Lighting Analysis Assistant. The scene must include a lighting solution before this tool is available. You can access this tool by selecting the Lighting Analysis menu command. This opens the Lighting Analysis Assistant dialog box, shown in Figure 45.16.

# Note

This feature is available only in 3ds Max 2010 Design.

In order for the Lighting Analysis Assistant tools to work, you need to have a lighting solution for the current scene, and you need to have mental ray enabled using real-world parameters and photometric lights. If any of these conditions aren't met, then it is indicated in the General panel and listed in bold. After making changes, you can press the Update Status button to recheck the settings. The General panel also includes a
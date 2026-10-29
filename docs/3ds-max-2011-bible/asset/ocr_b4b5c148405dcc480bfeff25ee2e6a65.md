# Chapter 20: Using Lights and Basic Lighting Techniques

rectangular. For a rectangular-shaped spotlight, you can control the aspect ratio. You can use the Bitmap Fit button to make the aspect ratio match a particular bitmap.

The Directional Light Parameters rollout, which appears for Direct light types, is identical to the Spotlight Parameters rollout and also includes settings for the Hot Spot and Falloff values.

# Advanced Effects

Options in the Affect Surface section of the Advanced Effects rollout control how light interacts with an object's surface. The Contrast value alters the contrast between the diffuse and the ambient surface areas. The Soften Diffuse Edge value blurs the edges between the diffuse and ambient areas of a surface. The Diffuse and Specular options let you disable these properties of an object's surface. When the Ambient Only option is turned on, the light affects only the ambient properties of the surface.

# Cross-Ref

Find more detail on the Diffuse, Specular, and Ambient properties in Chapter 15, “Using the Slate Material Editor.”

You can use any light as a projector; you find this option in the Advanced Effects rollouts. Selecting the Map option enables you to use the light as a projector. You can select a map to project by clicking the button to the right of the map option. You can drag a material map directly from the Material/Map Browser onto the Projector Map button.

# Shadow parameters

All light types have a Shadow Parameters rollout that you can use to select a shadow color by clicking the color swatch. The default color is black. The Density setting stands for “Density” and controls how dark the shadow appears. Lower values produce light shadows, and higher values produce dark shadows. This value can also be negative.

The Map option, like the Projection Map, can be used to project a map along with the shadow color. The Light Affects Shadow Color option alters the Shadow Color by blending it with the light color if selected.

In the Atmosphere Shadows section, the On button lets you determine whether atmospheric effects, such as fog, can cast shadows. You can also control the Opacity and the degree to which atmospheric colors blend with the Shadow Color.

When you select a light and open the Modify panel, one additional rollout is available: the Atmospheres and Effects rollout. This rollout is a shortcut to the Environment dialog box, where you can specify atmospheric effects such as fog and volume lights.

# Note

The only effects that can be used with lights are Volume Light and Lens Effects.

# Cross-Ref

Chapter 46, “Using Atmospheric and Render Effects,” covers atmospheric effects.

If the Area Shadows option is selected in the General Parameters rollout, then the Area Shadows rollout appears, which includes several settings for controlling this shadow type. In the drop-down list at the top of the rollout, you can select from several Basic Options, including Simple, Rectangle Light, Disc Light, Box
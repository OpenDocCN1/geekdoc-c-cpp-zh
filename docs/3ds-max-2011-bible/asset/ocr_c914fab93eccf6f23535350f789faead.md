# Part IV: Materials, Cameras, and Lighting Basics

# FIGURE 20.9

Using the Exclude/Include dialog box, you can exclude objects from casting shadows.

![](bbox=[0.08, 0.22, 0.58, 0.4])

# The Intensity/Color/Attenuation rollout

In the Intensity/Color/Attenuation rollout, the Multiplier value controls the light intensity. A light with a Multiplier set to 2 is twice as bright as a light with its Multiplier set to 1. Higher Multiplier values make a light appear white regardless of the light color. The Multiplier value can also be negative. A negative value can be used to pull light from a scene but should be used with caution.

# Tip

Adding and positioning another light typically is better than increasing the multiplier.

To the right of the Multiplier value is a color swatch. Clicking the color swatch opens a color selector where you can choose a new light color.

Attenuation is a property that determines how light fades over distance. An example of this is a candle set in a room. The farther you get from the candle, the less the light shines.

You use three basic parameters to simulate realistic attenuation. Near Attenuation sets the distance at which the light begins to fade, and Far Attenuation sets the distance at which the light falls to 0. Both these properties are ranges that include Start and End values. The third parameter sets the Decay value, which simulates attenuation using a mathematical formula to compute the drop in light intensity over time.

Selecting the Use option enables the Near and Far Attenuation values; both have Start and End values that set the range for these attenuation types. The Show option makes the attenuation distances and decay values visible in the viewports. The three types of decay from which you can choose are None, Inverse, and Inverse Square. The Inverse type decays linearly with the distance away from the light. The Inverse Square type decays exponentially with distance.

# Note

The Inverse Square type approximates real lights the best, but it is often too dim for computer graphic images. You can compensate for this by increasing the Multiplier value.

# Spotlight and directional light parameters

The Spotlight Parameters rollout includes values to set the angular distance of both the Hot Spot and Falloff cones. The Show Cone option makes the Hotspot and Falloff cones visible in the viewport when the light is not selected. The Overshoot option makes the light shine in all directions like an Omni light, but projections and shadows occur only within the Falloff cone. You can also set the light shape to be circular or
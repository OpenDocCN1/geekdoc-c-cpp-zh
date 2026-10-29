# Part IV: Materials, Cameras, and Lighting Basics

and Rotate transform button. Spotlights always are displayed in the viewport as a cone with the light positioned at the cone apex.

# Cross-Ref

**Both Target Spot and Target Direct lights are very similar in functionality to the Target Camera object, which you learn about in Chapter 19, “Configuring and Aiming Cameras.”**

# Direct light

Direct lights cast parallel light rays in a single direction, like the sun. Just like spotlights, direct lights come in two types: a Target Direct light and a Free Direct light. The position of the Target Direct light always points toward the target, which you can move within the scene using the Select and Move button. A Free Direct light can be rotated to determine where it points. Direct lights are always displayed in the viewport as cylinders.

# Skylight

The Skylight is like a controllable ambient light. You can move it about the scene just like the other lights, and you can select to use the Scene Environment settings or select a Sky Color.

# Area Omni and Area Spot

The Area lights project light from a defined area instead of from a single point. This has the effect of casting light along a wider area with more cumulative intensity than a point light source. Area lights are supported only by the mental ray renderer. If you use the Scanline renderer, these lights behave like simple point lights.

The Area Omni light lets you set its shape as a Sphere or a Cylinder in the Area Light Parameters rollout. Area Spot lights can be set to be either Rectangular or Disc-shaped. Be aware that area lights can take significantly longer to render than point lights.

# Cross-Ref

**For more details on the mental ray renderer, see Chapter 47, “Rendering with mental ray.”**

# Photometric lights

The standard Max lights rely on parameters like Multiplier, Decay, and Attenuation, but the last time I was in the hardware store looking for a light bulb with a 2.5 Multiplier value, I was disappointed. Lights in the real world have their own set of measurements that define the type of light that is produced. Photometric lights are lights that are based on real-world light measurement values such as Intensity in Lumens and temperatures in degrees Kelvin.

If you select the Lights menu or the Lights category in the Create panel, you’ll notice another subcategory called Photometric. Photometric lights are based on photometric values, which are the values of light energy. The lights found in this subcategory include Free and Target lights.

# Cross-Ref

**The Photometric category also includes a mr Sky Portal option that is used to focus lights coming in from an external source. This feature is covered in Chapter 47, “Rendering with mental ray.”**
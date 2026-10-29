+   - **Uniform Diffuse:** This distribution type spreads light equally in all directions for only one hemisphere, such as when a light is positioned against a wall.
+   - **Spotlight:** This distribution type spreads the light in a cone shape, like a flashlight or a car's headlight.
+   - **Photometric Web:** This distribution type can be any arbitrary 3D representation and is defined in a separate file that can be obtained from the light manufacturer and loaded into the light object. Once loaded, the distribution graph is visible in the Distribution rollout.

The Uniform Spherical option distributes light equally in all directions. The Uniform Diffuse option has its greatest distribution at right angles to the surface it is emitted from and gradually decreases in intensity at increasing angles from the normal. For both options, the light gradually becomes weaker as the distance from the light increases.

The Spotlight option concentrates the light energy into a cone that emits from the light. This cone of light energy is directional and can be controlled with the Hotspot and Falloff values.

The Photometric Web option is a custom option that lets you open a separate file describing the light's emission pattern. These files have the .ies, .cibse, or .lti extensions. Light manufacturers have this data for the various real-world lights that they sell. You load these files using the Choose Photometric File button found in the Distribution (Photometric Web) rollout. You can also specify the X-, Y-, and Z-axis rotation values.

# Color options

The Color section of the Intensity/Color/Attenuation rollout, shown in Figure 20.10, includes two ways to specify a light's color. The first is a drop-down list of options. The options found in the list include standard real-world light types such as Cool White, Mercury, and Halogen. Table 20.2 lists each of these types and its approximate color.

# FIGURE 20.10

The Intensity/Color/Attenuation rollout for photometric lights uses real-world intensity values.

![](bbox=[0.03, 0.9, 0.22, 0.99])
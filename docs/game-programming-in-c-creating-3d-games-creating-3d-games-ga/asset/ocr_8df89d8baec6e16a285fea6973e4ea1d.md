as before.

# Exercise 13.2

Adding a new type of light to deferred shading requires a new type of light geometry. Add support for spotlights. To do so, you need to create a SpotLightComponent as well as a corresponding shader to draw these lights after the point lights.

Use the provided SpotLight.gpmesh file (which is a cone) as the mesh for spotlights. A spotlight should have parameters like those of a point light, but it also needs a variable for its angle. To be able to change the angle, the mesh needs to also scale non-uniformly. The default mesh has a half angle of 30 degrees.
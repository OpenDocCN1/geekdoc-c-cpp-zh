![](bbox=[0.19, 0.11, 0.46, 0.27])

Figure 12.13 Structured Illumination

regular, two-camera stereopsis problem and replace one of those cameras by a projector that shines a very narrow, very bright slit on the scene, as illustrated in Figure 12.13. Now, one angle, \(\theta\), is known from the projector; the other angle, \(\phi\), is measured by finding the bright spot in the camera image, counting over pixels, and knowing the relationship between pixels and angle. Finally, knowledge of the distance between cameras, \(d\), makes the triangle solvable. An interesting problem occurs when one uses structured illumination to look at specular reflectors such as metal surfaces. With specular reflectors, either not enough or too much light may be reflected (polarization filters help [12.35]).

# 12.5.1 Structured Illumination – An Example

The key to doing structured illumination is to realize that by controlling the lighting, one or more of the unknowns in the stereopsis problem may be eliminated. Let’s look at an example in more detail to see how this might work.

The problem to be solved is an application in robot vision: a robot is to pick up shiny, metallic turbine blades from a cart and place them into a machine for further processing. In order to locate the blades, a horizontal slit of light is projected onto the scene, by passing a laser beam through a cylindrical lens. The geometry of the resulting images is illustrated in Figure 12.14. If there were no blade in the image, the light stripe from the laser would form

![](bbox=[0.19, 0.71, 0.5, 0.87])

Figure 12.14 In an application requiring structured illumination to locate turbine blades, the presence of a blade translates the location of the light stripe vertically in the image. (From [12.35])
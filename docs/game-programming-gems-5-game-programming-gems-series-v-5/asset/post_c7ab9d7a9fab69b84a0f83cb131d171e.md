
## Back of the Envelope Aerodynamics for Game Physics

Graham Rhodes, Applied Research Associates, Inc.
grhodes@nc.rr.com

In real life, aerodynamics enable heavier-than-air vehicles to fly, make the curve ball possible, and cause palm trees to sway above beautiful girls on exotic beaches. Aerodynamics have long played a role in gaming, primarily in flight simulators, and in some cases have been used to improve the realism of effects such as particle systems. Many game developers take an ad-hoc approach to aerodynamics that is based more on numerical experimentation than on sound principles. This gem will provide a portfolio of simple, low-CPU/GPU-cost, back-of-the-envelope formulas, derived from sound engineering principles and strictly controlled wind-tunnel experiments, that game programmers can use to support a wide variety of aerodynamic effects in many game genres. While we use the term aerodynamics, in fact the formulas here work equally well for objects moving through a fluid such as water, as long as velocities are fairly high.

The gem is developed in two sections. The first section describes how different aerodynamic primitives can serve as proxies to game geometry and presents simple equations for calculating aerodynamic forces on those primitives. You can reasonably use these equations for objects that are moving through the air or other fluids at a Mach number of less than approximately 0.75. While the presentation is short on theory due to limited print space, certain key principles from aerodynamics theory are present. The second section of the gem focuses on applications of back-of-the-envelope aerodynamics to achieve way cool effects in action games, complete with source code.

## Background

The following sections provide some background on the topic of aerodynamics.

## Aerodynamic Loads and Rigid Body Dynamics

The formulas presented herein will help you to calculate approximate aerodynamic loads—forces and moments (also known as torque)—that can be applied to rigid bodies. The loads calculated with these formulas can simply feed your existing rigid body physics system!

In the engineering world of aircraft flight dynamics, there are six standard aerodynamic load quantities: three forces (lift, drag, and side force, which is perpendicular to the other two) and three moments (pitching moment, yawing moment, and rolling moment). However, the manner in which this gem treats geometry allows us to simplify the situation, modeling only lift, drag, and a single moment. The full set of three forces and three moments is simply a generalization. Figure 4.1.1 illustrates the orientation of these three load quantities.

![](img/672fe9a2d008ba627b1991e15d70f43e_437_0.png)

FIGURE 4.1.1 Location and orientation of lift, drag, and pitching moment. Drag acts in the direction of the relative wind, and lift acts perpendicular to the relative wind—both often through a location other than the center of gravity. Pitching moment acts about an axis through the center of gravity and perpendicular to the lift/drag plane.

Here, the axis system Xw, Zw represents the world space coordinate system, and the axis system Xo, Zo represents an object-aligned coordinate system. For 3D objects, there are of course Yw and Yo directions, and the two coordinate systems will often be more arbitrarily oriented. The object’s orientation is unimportant as long as it is known. The orientation of the relative wind, defined later, is critical to calculation of the forces.

The orientation of these loads, which are defined here in the so-called *wind axes*, may surprise you. You may have been expecting the lift force to act vertically straight up (opposite gravity) and the drag force to act horizontally—both acting through the center of gravity, since many simplistic introductions to aerodynamics present the forces in this way. You may have never heard of pitching moment. Be assured, the wind axis representation is both realistic and fundamental to simple aerodynamic theory.

The force calculations depend only on the object's orientation relative to the wind and not to the world. While lift on airplane wings normally does have a vertical component that balances the object's weight, causing the object to move horizontally or with a constant vertical velocity, lift can in fact act in any direction, even horizontally! It is recognition of this that makes it reasonable for us to ignore the side force, for example, as a special case, since side force is often just a horizontally oriented lifting force.

## Dimensionless Forms

It is common practice to represent all the aerodynamic loads in terms of dimensionless coefficients. Equations 4.1.1 through 4.1.3 are equations for computing the loads given the value of a dimensionless coefficient.

```
D = Drag = \frac{\rho V^2 S_{ref} C_D}{2} \quad (4.1.1)

L = Lift = \frac{\rho V^2 S_{ref} C_L}{2} \quad (4.1.2)

M = Pitching Moment = \frac{\rho V^2 S_{ref} l_{ref} C_M}{2} \quad (4.1.3)
```

Here, $C_D$ is the drag coefficient, $C_L$ is the lift coefficient, and $C_M$ is the pitching moment coefficient. The variable $S_{ref}$ is a constant reference area, usually taken to be a projected area of the geometry, such as a cross-section area or a top-down projected area. The variable $l_{ref}$ is a reference length, usually taken to be one of the physical dimensions of the object, such as the chord width of a wing or the diameter of a sphere-like object. The variable $\rho$ is the fluid density, which for gaming applications will most often be taken to be constant.

Finally, the variable $V$ is the speed of the fluid, measured relative to the object, that is, it is the speed the fluid moving past the object, measured in world space. Given the velocity of the point on the body where the force is applied to an object, $\vec{V}_{location-of-force}$, in world space, and a wind velocity in world space, $\vec{V}_{wind}$, it is easy to find the wind velocity relative to the object, $\vec{V}_{relative\_wind}$, using Equation 4.1.4. The geometry of this situation is illustrated in Figure 4.1.2. The quantity $V$ in Equations 4.1.1 through 4.1.3 is simply the magnitude of $\vec{V}_{relative\_wind}$. When calculating $\vec{V}_{location-of-force}$, be sure to include the translational velocity due to object rotation, since this will affect the forces. Specifically, let $\vec{V}_{location-of-force} = \vec{V}_{point-of-rotation} + (\vec{\omega} \times (\vec{V}_{location-of-force} - \vec{V}_{point-of-rotation}))$, with $\vec{r}$ being the location of a point, measured in world space, and $\vec{\omega}$ being the rotational velocity about an axis through the point $\vec{V}_{point-of-rotation}$, measured in radians per second, as shown in Equation 4.1.4.

$\vec{V}_{relative\_wind} = \vec{V}_{wind} - \vec{V}_{location-of-force}$ (4.1.4)

![](img/672fe9a2d008ba627b1991e15d70f43e_439_0.png)

## Fluid Properties and the Standard Atmosphere

The equations presented herein are dependent on the fluid properties, be that fluid air, water, or something else. At sea level, air has an average density, \(\rho\), of 1.225 kg/m\(^3\) (23.77 × 10^{-4} slugs/ft\(^3\)), and dynamic viscosity, \(\mu\), of 1.789 × 10^{-5} Newton-seconds/m\(^3\) (3.737 × 10^{-7} lb-seconds/ft\(^2\)). At 20 degrees Centigrade, pure water has an average density of 1000 kg/m\(^3\) (1.94 slugs/ft\(^3\)) and a dynamic viscosity of 1.0 × 10^{-3} Newton-seconds/m\(^2\) (2.09 × 10^{-5} lb-seconds/ft\(^2\)).

For air, at any given moment in time, the properties vary with altitude, as well as with weather conditions, etc. There is a model, called the _Standard Atmosphere_ (U.S. and International versions) exist, which represents the average air properties over a range of altitudes. An Internet search on that phrase will produce numerous links, including table listings of the properties and software for querying the tables.

## Aerodynamic Primitives

While there have been a few developments that simulate variants of the _Navier-Stokes_ equations of fluid flow in real time [Stam03, Lander02], for the purpose of simulating

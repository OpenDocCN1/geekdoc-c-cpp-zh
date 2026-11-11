
rotational plane of the tire. The tire as a whole is driven by the wheel, the axle, and ultimately the drive train and engine to rotate. Because the point of contact resists motion in the plane of the road, that frictional force propagates backward through the system and produces a net linear acceleration of the car along the road. On ice or in mud there is little friction between a tire and the road. In this case, the points on the tire can move freely relative to the road, so the car does not move.

A similar situation applies to turning a car. At the point of contact, high friction along the axis of the axle resists motion along that axis, while lower friction perpendicular to the axis of the car’s wheel allows motion. This creates a net rotation of the car. Thus, in the broader sense, friction can be essential for enabling motion.

Frictional forces arise from electrostatic repulsion and attraction. In the repulsion case, molecules of adjacent surfaces collide. As we saw when studying BSDFs, surfaces that are macroscopically planar may be microscopically rough. Thus, what appears to be two smooth surfaces sliding parallel to each other may actually more closely resemble the meshed teeth of two long linear gears. This is why rougher surfaces increase friction. It is also why the sole of a new dress shoe is slipperier. That sole is a relatively smooth piece of leather. After the shoe has been worn, say, by walking on concrete sidewalks for a few days, the leather sole exhibits small bumps and cracks from uneven wear. These mesh with bumps on the ground and create greater friction.

In the attraction case, materials of different surfaces chemically bond with each other when in contact, and resist being pulled apart. The bonding is often strongest when the two materials are the same. This is why smooth glass slides easily on smooth wood but is hard to drag across another piece of smooth glass (try this with two juice glasses at breakfast!).

There are case-specific models of friction for commonly arising scenarios. We present two here. Dry friction occurs between solids moving parallel to the plane of contact, and drag occurs between a solid and a fluid.

In the dry friction model, the force is factored into static and kinetic (a.k.a. dynamic) terms. Let the two objects be numbered 1 and 2. We consider the force on object 1 in the reference frame of the combined system. That is, the center of mass of both objects combined will always be at rest.

Static friction is zero when object 1 is moving, that is, when \(\dot{x}(t) \neq 0\) in the system’s frame. When object 1 is still relative to the reference frame of the system and is in contact with object 2 only along a surface, then we model static friction as able to resist acceleration due to net forces up to

\[
k = \mu_s \|\mathbf{F}_n\| \qquad (35.43)
\]

parallel to the surface. That is, if the net force is \(\mathbf{f}\), then the object will experience no acceleration in the plane of the surface if \(\|\mathbf{f}\| - |\mathbf{f} \cdot \mathbf{n}| < k\). Otherwise, it will experience some acceleration and kinetic friction as described shortly.

The coefficient of static friction \(\mu_s\) is determined by the chemical composition of the two surfaces, the amount of surface area in contact, and the microgeometry of the surfaces. In other words, there are a lot of hidden parameters in the static friction equation. However, the coefficient is often approximated as a constant material property in simple simulations.

When two objects already have relative velocity with respect to each other in the plane of their contact, we model kinetic friction. Kinetic friction has lower magnitude than the static friction threshold. This is because objects that are already in motion tend to be bouncing away from their plane of contact at a microscopic scale. Small bounces preclude many of the surface interactions, both chemical and mechanical, that cause friction.

We model kinetic friction (Figure 35.25) as a force

\[
\mathcal{F}_{\mathrm{fr}}(t,\mathbf{x},\mathbf{v}) = -\mu_k \|\mathcal{F}_n\| \frac{\mathbf{v}}{\|\mathbf{v}\|}, \qquad (35.44)
\]

![](img/f464cd0043eb5336aa0543fe20a0561b_1058_0.png)

… but we must be careful in simulation to never reverse direction of velocity in a time step due to frictional forces. This constraint must be enforced by the integrator or at least with knowledge of the integrator’s time steps.

**Drag** is the frictional force on a moving object (Figure 35.26) due to the surrounding fluid medium, which is often water or air. Lord Rayleigh’s model of drag is a force,

\[
\mathcal{F}_d(t,\mathbf{v}) = -\frac{1}{2}\rho\|\mathbf{v}\|aC_d\mathbf{v}, \qquad (35.45)
\]

where \(a\) is the surface area of the object presented along the direction of motion; \(C_d\) is the drag coefficient, which depends on the shape of the object, its roughness, and the chemical composition of the materials; and \(\rho\) is the density of the fluid. As with other frictional forces, we must be careful that the drag force does not reverse the direction of motion during a time step.

Drag force leads to two particularly interesting macroscopic phenomena. The first is **terminal velocity**. An object falling through a medium does not experience continual net acceleration. For example, a skydiver’s velocity levels off during freefall. This occurs because at some point \(\mathcal{F}_g = -\mathcal{F}_d\), since \(\mathcal{F}_d\) is proportional to velocity but \(\mathcal{F}_g\) is constant on the object.

![](img/f464cd0043eb5336aa0543fe20a0561b_1058_1.png)

**Lift** is another interesting phenomenon. An airfoil moving through a fluid experiences a net upward force, which allows airplanes and birds to rise in the absence of updrafts. Bernoulli’s principle describes how lift arises from variations in drag force over the entire surface. As was the case with a car tire, friction is paradoxically *enabling* motion in this case—just not motion in the direction that the friction opposed.

## 35.6.4.6 Other Forces

There are of course other fundamental real-world forces: for example, magnetic, strong and weak nuclear, and electrical. These can be adopted from a physics textbook in the same manner as the ones described here. There are also nonfundamental forces that are useful modeling techniques, such as tension and compression, that can be found in any mechanical engineering text.

Nonphysical forces, such as tractor and repulsor beams in a science fiction context, can be described using arbitrary functions. Any force desired can be inserted into the simulation framework, since Newton’s first law of motion reduces it to an acceleration that can be inserted into the integrator.

## 35.6.5 Particle Collisions

### 35.6.5.1 Collision Detection

For particles with very small cross sections, collision detection is equivalent to ray tracing. We can ignore the collisions between particles because the probability of those collisions occurring is vanishingly small. The path of a particle over a sufficiently small time interval is a line segment, so by tracing a ray from the particle’s origin in the direction of its velocity we can detect collisions with other parts of the scene. All of the data structures and algorithms built for tracing light rays can thus be applied to dynamics simulation.

It is also possible to model collisions between particles with volume while simulating the movement of each particle as if it were a point mass. To detect a general intersection between two particles we choose the reference frame of one (so that it is not moving), and then extrude the other one along the relative velocity vector. For particles with spherical bounds the intersection test is relatively simple because it is equivalent to testing whether a point is inside a capsule (a cylinder with a hemispherical cap on each end). Collisions between other shapes are often more difficult to compute, and the best solution can be to use a spatial data structure to detect intersecting polygons (see Chapter 37).

### 35.6.5.2 Normal Forces through Transient Constraints

After a collision is detected, the system must respond to prevent particles from penetrating the scene. We’ve already seen one response—normal forces. When a collision occurs between objects with very low velocity toward each other, it is likely due to resting contact. In this case, reacting to the collision by reversing velocity might introduce energy into the system, since the “collision” itself is an artifact of limited numerical precision for times and positions: Two objects in resting contact should never have accelerated toward each other in the first place. We can restore stability by explicitly moving the objects out of contact or applying normal forces to prevent penetration before it occurs.

We’ve seen that normal forces can be tricky to apply because they must occur “after all other forces” . . . which leads to an awkward ordering constraint when normal forces from multiple surfaces are in effect. In systems with a sophisticated integration scheme, it is possible to apply normal forces implicitly rather than explicitly. In these cases, contact creates a temporary “joint” between two objects, requiring that the solution to the simulation during the time step must not move the point of contact on either object [L68].

### 35.6.5.3 Penalty Forces

A generalization of normal forces can elegantly resolve collisions between objects with significant velocities. A **penalty force** is something like a normal force. It applies to objects that are interpenetrating. The magnitude of a penalty force increases with the level of penetration, and the direction is that which will most quickly separate them. This is actually a reasonable model for microscopic electrostatic repulsion. Atoms never really contact one another. As they come close, they repel each other with increasing strength until the relative velocities reverse and the proximity decreases. When the force is integrated over the time period from when the penalty force first becomes significant to when it again becomes insignificant, the net result is that of an elastic collision: The velocities of the objects have been reflected about the normal to the plane of their “collision.”

Penalty forces are simple to compute and apply, but often difficult to tune. If the penalty force is too weak, then objects will interpenetrate too far before rebounding. This gives the appearance of overly rubbery materials. If the penalty force is too strong, then any inaccuracy in the integration process can destabilize the system by creating energy due to undersampling. When there are multiple potential points of contact, uneven application of penalty forces due to differing

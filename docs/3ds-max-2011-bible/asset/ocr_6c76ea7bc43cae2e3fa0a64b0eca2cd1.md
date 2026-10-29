# Defining collision boundaries

Another common property that you can set pertains to how the object deals with collision detection. You can select the volume to use to determine when two objects collide with each other. If this sounds a bit funny because any collision volume that doesn’t use the actual mesh would be inaccurate, then you need to realize that a complex simulation with lots of collisions of complex objects could take a long time to compute. If reactor has only to compute collisions based on the object’s bounding box instead of the actual mesh object, the simulation runs much more quickly and the inaccuracies aren’t even noticeable.

Before deciding on the collision boundary to use, you need to determine whether an object is convex or concave. A concave object is one that you can penetrate with a ray and cross its mesh boundary only twice. Convex objects require more than two crossings with an imaginary ray. You can test whether an object is convex using the Animation ▸ reactor ▸ Utilities ▸ Convexity Test menu command or in the Utils rollout of the Utilities panel with a button named Test Convexity.

A convex object can use any of the options found in the Simulation Geometry rollout of the Object Properties dialog box, including Bounding Box, Bounding Sphere, Mesh Convex Hull, Proxy Convex Hull, Concave Mesh, Proxy Concave Mesh, or Not Shared as its collision boundary. If a Proxy option is selected, you can select the proxy object using the Proxy button found in the Simulation Geometry rollout. A proxy is a just a low-resolution version of an object used here for collision detection.

# Note

The Material Editor includes a Dynamics Properties rollout with values for Bounce Coefficient, Static, and Sliding Friction. These values are used with the Dynamics utility but are not used with the reactor engine.

# Modifier properties

In addition to the properties found in the Property Editor, objects that have one of the reactor modifiers applied to it have additional properties that are specific to the collection types. These properties show up in the Modify panel when the object is selected.

# Note

All the modifiers include an option to Avoid Self-Intersections. Because these object types are flexible, they often move and bunch up together. This option prevents an object from turning inside out and intersecting with itself.

For the Cloth modifier, these additional properties include Mass, Friction, Relative Density, and Air Resistance. You can also select to use the Simple Force Model or the Complex Force Model, which enables Stretch, Bend, Shear, and Damping values. You can also define a Fold Stiffness, which determines how stiff the fold in the cloth is.

# Note

When similar properties exist for an object in the Property Editor and the Modify panel, the value in the Modify panel takes precedence. Actually, the properties in the Property Editor apply only to rigid body objects.

The Soft Body modifier adds value for Stiffness and Damping to the Mass and Friction values. You can also select to have the object deform using a Mesh-based or (Free Form Deformer) FFD-based algorithm. The FFD-based algorithm uses control points and is a simpler method that doesn’t require as much memory.

The Rope modifier includes Mass, Thickness, Friction, and Air Resistance values. You can also select the rope to be a Spring or Constraint type. Spring ropes act like bungee cords or rubber bands.
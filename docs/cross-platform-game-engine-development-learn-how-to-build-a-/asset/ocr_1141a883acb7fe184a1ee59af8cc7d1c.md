# # Rigid Body

A rigid body is a solid object on which external force causes no deformations. The assumption that there is no deformation to the body simplifies the analysis by reducing the number of parameters required to perform a realistic simulation. The idea is to make our player, or any object affected by gravity for collision handling and more.

# ## Cinematics

Before we can create any component or system, we first need to understand how rigid bodies behave in an environment. We won't get too deep into this topic, but we will briefly talk about the necessary stuff. In the real world, rigid bodies are described using three dimensions (x, y, and z), but because the focus of this book is to deal with 2D-games, we won't use the third dimension in our simulations. The following table describes how rigid body's parameters are related to each other for linear uniform motions.

| Parameters | Equations |
| :--- | :--- |
| Acceleration [m/S²] | a = (F + Fr + Fg)/m |
| Velocity [m/s] | V = a * t + V0 |
| Position [m] | P = V * t + P0 |

Each parameter in the table above is a 2D-vector with (x, y) components.

# ### Acceleration (a)

In mechanics, acceleration is the rate of change of the velocity of an object with respect to time. Accelerations are vector quantities (in that they have magnitude and direction). The orientation of an object's acceleration is given by the orientation of the net force acting on that object. The magnitude of an object's acceleration, as described by Newton's Second Law, is the combined effect of two causes [21]:

+   * The net balance of all external forces acting onto that object — magnitude is directly proportional to this net resulting force.
+   * That object's mass, depending on the materials out of which it is made — magnitude is inversely proportional to the object's mass

# ### Velocity (V)

The velocity of an object is the rate of change of its position with respect to a frame of reference and is a function of time. Velocity is equivalent to a specification of an object's speed and direction of motion (e.g., 60 km/h to the
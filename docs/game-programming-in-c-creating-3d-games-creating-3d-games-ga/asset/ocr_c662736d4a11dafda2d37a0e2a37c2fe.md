You can use a similar float variable in `Laser` to force the laser to die (and be deleted from the game world) after one second, even if the laser doesn't collide with an asteroid.

# SUMMARY

A vector represents a magnitude and a direction. You can use vectors for many different computations, including creating a vector between two points (using subtraction), calculating the distance between two points (using subtraction and length), finding the angle between two vectors (using the dot product), and calculating a normal to a surface (with the cross product).

For basic movement, this chapter shows how to create a `MoveComponent` that allows actors to move in the forward direction as well as rotate. For forward movement, you multiply the forward vector of the actor by movement speed and delta time. Adding this to the current position of the actor yields the new position of the actor after the time step. In this chapter you also learned how to add support for overridable input behavior in actors and components, and how to leverage this to create an `InputComponent` that inherits from `MoveComponent`.

In Newtonian physics, the acceleration of an object is force applied to the object divided by the object's mass. You can use Euler integration to calculate the change in
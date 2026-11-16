Figure 3.16 Triangle for problem 2 of Exercise 3.1

3. Suppose a 2D game features an arrow that points from the player to the next objective.

When the game first begins, the arrow points down the x-axis <1,0>.

The player's initial position is at (4,0).

You create a new object at the position (5,6).

+   a. What is the unit vector from the player's initial position to the new waypoint?

+   b. Calculate the angle of rotation between the initial arrow direction and the vector calculated in part (a).

+   c. Calculate the vector perpendicular to the plane created by the initial arrow direction and the vector calculated in part (a).

# Exercise 3.2

Currently, the ship does not collide against asteroids in the chapter game project. Add collision for the ship. To do so, you first need to create a CollisionComponent in Ship and specify a radius. Next, in Ship::UpdateActor, you need to test against the collision of all asteroids (much the way the laser does). If the ship collides with an asteroid, force it to reset in the center of the screen with a rotation of zero.

As an extra feature, make it so the ship disappears for a
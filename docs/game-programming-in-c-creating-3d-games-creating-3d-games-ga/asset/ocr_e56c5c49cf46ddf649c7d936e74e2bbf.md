Numeric integration allows a game to update the velocity based on the acceleration and then update the position based on the velocity. However, to compute the acceleration of an object, the game needs to know the mass of the object as well as the forces applied to the object.

There are multiple types of forces to consider. Some forces, such as gravity, are constant and should apply on every frame. Other forces may instead be **impulses**, or forces that apply only for a single frame.

For example, when a character jumps, an impulse force allows the player to get off the ground. However, the character will eventually return to the ground because of the constant force of gravity. Because multiple forces can act on an object simultaneously, and forces are vectors, adding up all the forces gives the total force applied to an object for that frame. Dividing the sum of forces by mass yields acceleration:

Click here to view code image

```
acceleration = sumOfForces / mass;
```

Next, you can use the **Euler integration** method of numeric integration to compute the velocity and the position:

Click here to view code image

```
// (Semi-Implicit) Euler Integration
```

angular speed.

## Listing 3.5 InputComponent::ProcessInput Implementation

Click here to view code image

```
void InputComponent::ProcessInput(const uint8_t* keyState
{
    // Calculate forward speed for MoveComponent
    float forwardSpeed = 0.0f;
    if (keyState[mForwardKey])
    {
        forwardSpeed += mMaxForwardSpeed;
    }
    if (keyState[mBackKey])
    {
        forwardSpeed -= mMaxForwardSpeed;
    }
    SetForwardSpeed(forwardSpeed);
    // Calculate angular speed for MoveComponent
    float angularSpeed = 0.0f;
    if (keyState[mClockwiseKey])
    {
        angularSpeed += mMaxAngularSpeed;
    }
    if (keyState[mCounterClockwiseKey])
    {
        angularSpeed -= mMaxAngularSpeed;
    }
    SetAngularSpeed(angularSpeed);
}
```

With this in place, you can then add keyboard-controlled movement to Ship by simply creating an InputComponent instance. (We omit the code for the Ship constructor here, but it essentially sets the various InputComponent member variables for the keys and maximum speed.) You also create a SpriteComponent and assign it a texture. This yields a user-controllable ship (see Figure 3.12).

![](img/e9afcec1487716b0ef80d7e7c09869c8_210_0.png)

Figure 3.12 Ship controlled with the keyboard

This is an excellent first pass of a more flexible system for input. We explore input in much greater detail in Chapter 8, “Input Systems.”

## NEWTONIAN PHYSICS

Although the basic movement approach used so far in this chapter works for some games, for movement that more closely resembles the real world, you need a physically accurate approach. Luckily, Isaac Newton (among others) developed Newtonian physics (or classical mechanics) to describe laws of motion. Games commonly utilize Newtonian physics because its laws hold if objects are not moving near the speed of light and objects are larger than quantum particles. Because games typically don't feature objects in those edge cases, Newtonian physics works well.

There are several different aspects to Newtonian physics. This book considers only the most basic: movement without rotational forces, or linear mechanics. For deeper discussions of other components of Newtonian physics, consult either Ian Millington’s book, listed in this chapter’s “Additional Reading” section, or any college-level physics textbook.

## Linear Mechanics Overview

The two cornerstones of linear mechanics are force and mass. Force is an influence that can cause an object to move. Because force has a magnitude and direction, it’s natural to represent force with a vector. Mass is a scalar that represents the quantity of matter contained in an object. It’s common to confuse mass with weight, but mass is independent of any gravity, whereas weight is not. The greater the mass of an object, the more difficult it is to change the movement of that object.

If you apply sufficient force to an object, it will start moving. Newton’s second law of motion encapsulates this idea:

```
F = m · a
```

In this equation, F is force, m is mass, and a is acceleration, or the rate at which the velocity of an object increases. Because force equals mass times acceleration, it's also true that acceleration is force divided by mass. This is the usual approach in games: An arbitrary object in the game has a mass, and you can apply forces to that object. From this, you can then compute the acceleration of the object.

In a physics course, the typical symbolic representation of linear mechanics is that position, velocity, and acceleration are functions over time. Then, with calculus, you can calculate the velocity function as the derivative of the position function and the acceleration function as the derivative of the velocity function.

However, this standard formulation in terms of symbolic equations and derivatives is not particularly applicable in a game. A game needs to apply a force to an object and, from that force, determine the acceleration over time. Once you have an object's acceleration, you can compute the change in the object's velocity. Finally, given a velocity, you can compute the change in the object's position. A game only needs to compute this in terms of the discrete time step of delta time. It doesn't need a symbolic equation. This requires using integration—but not symbolic integration. Instead, you must use **numeric integration**, which approximates the symbolic integral over a fixed time step. Although this sounds very complex, luckily, you can accomplish numeric integration with only a few lines of code.

## Computing Positions with Euler Integration

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
// Update velocity
velocity += acceleration * deltaTime;
// Update position
position += velocity * deltaTime;
```

Note that force, acceleration, velocity, and position are all represented as vectors in these calculations. Because these calculation depend on the delta time, you can put them in the `Update` function of a component that simulates physics.

## Issues with Variable Time Steps

For games that rely on physics simulation, variable frame times (or **time steps**) can cause problems. This is because the accuracy of numeric integration depends on the size of the time step. The smaller the time step, the more accurate the approximation.

If the frame rate varies from frame to frame, so does the accuracy of the numeric integration. The accuracy changing could affect the behavior in very noticeable ways. Imagine playing *Super Mario Bros.*, where the distance Mario can jump varies depending on the frame rate. The lower the frame rate, the further Mario can jump. This is because the error amount in numeric integration increases with a lower frame rate, which results in an exaggerated jump arc. This means that the game played on a slower machine allows Mario to jump farther than the game played on a fast machine. Figure 3-13 illustrates an example where the actual simulated arc diverges from the intended arc due to a large time step.

![](img/e9afcec1487716b0ef80d7e7c09869c8_215_0.png)

Figure 3.13 The actual jump arc diverges from an intended jump arc due to a large time step

For this reason, any game that uses physics to calculate the positions of objects should not use a variable frame rate—at least not for the physics simulation code. Instead, you can use the frame-limiting approach, as in Chapter 1, which works if the frame rate doesn't go below the target frame rate. A more complex alternative is to divide the larger time step into multiple fixed-size physics time steps.

## BASIC COLLISION DETECTION

**Collision detection** is how a game determines whether two objects in the game world touch each other. In Chapter 1, you implemented a form of collision detection to determine whether the ball collided with the wall or paddles. However, for the Asteroids game project in this chapter, you need slightly more complex calculations to decide whether the lasers the ship fires should collide with the asteroids in the game world.

A key concept in collision detection is simplification of the problem. For example, the asteroid image is circular but not exactly a circle. While it is more accurate to test collision against the actual contours of the asteroid, it's far more efficient to consider the asteroid as a circle for the purposes of collision detection. If you similarly simplify the laser into a circle, you then only need to determine whether these two circles collide.

## Circle-Versus-Circle Intersection

Two circles intersect with each other if and only if the distance between their centers is less than or equal to the sum of their radii. Figure 3.14 demonstrates this between two circles. In the first case, the two circles are far enough apart that they do not intersect. In this case, the distance between their centers is greater than the sum of the radii. However, in the second case, where the circles do intersect, the distance between their centers is less than the sum of their radii.

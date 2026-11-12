We start by checking if "game_over" is set to true. If not, we check if the player's rigid body is disabled. That only happens when the player has collided with either a pipe or the ground. When that happens, we

![](bbox=[0.08, 0.12, 0.43, 0.55])

have to make sure that the ground motion is stopped by disabling its rigid body. We also stop all pipe motion by disabling their rigid bodies as well.

If the plane is still flying, we call the update function to move our pipes. We then check if 2 seconds have passed. If that's the case, we will create another pair of pipes using the "spawn_pipe" function.

# Figure 43 Behind the scenes

Figure 43 shows what happens behind the scenes when the game is running. The pipes are created outside of the screen viewport, and because of the rigid bodies, they will start moving towards the player. Every time we create a pair of pipes, we set the value of the time back to zero to restart the cycle as long as the player is alive.

If you compile your project, you will be able to see the pipes being created.
# Unity Games by Tutorials

```
jumpDuration += Time.deltaTime;
}\else{
  isJumping = false;
  jumpDuration = @f;
}
```

As long as the jump button is held down, jumpDuration is counted using the time the previous frame took to complete (Time.deltaTime). If jump is released, jumpDuration is set back to 0 for the next time it needs to be timed, and the isJumping boolean flag is set back to false.

Save your code, and run the game to try it out (tap or hold Space to test the different jump heights).

![](bbox=[0.195, 0.355, 0.804, 0.467])

# Handling air control

When Super Soy Boy is in the air, you don't want him to handle as quickly as he normally does when he runs along the ground, so you'll now change the acceleration variable based on whether the player is in the air or not.

Firstly, seeing as you have the PlayerIsOnGround() Boolean check method available, in the FixedUpdate() method, check the if (input.x == 0) line to:

```
if (PlayerIsOnGround() && input.x == 0)
```

This is an extra check to ensure that xVelocity is only set to 0 if the player is on the ground and not using left or right controls.

Add a new variable to the top of the class to hold a value that will be used for air control:

```
public float airAccel = 3f;
```

The value of 3f for airAccel is half the value of the normal accel value. You already accel for ground movement, and will now use airAccel for air control. This means that air control will no longer be as twitchy as control so jumps will not be too difficult or frustrating for players (jump over-compensation).
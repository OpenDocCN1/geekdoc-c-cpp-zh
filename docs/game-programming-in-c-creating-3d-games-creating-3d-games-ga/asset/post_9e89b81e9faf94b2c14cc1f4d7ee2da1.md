
stick is at rest, the values reported for the stick's x- and y-axes are zero. However, in practice the values will be around zero but rarely precisely zero. Conversely, if the player slams the stick all the way to the right, the value reported by the stick's x-axis will be near the maximum value but rarely precisely the maximum value.

This is problematic for games for two reasons. First, it may cause **phantom inputs**, where the player isn't touching an input axis but the game reports that something is happening. For example, suppose the player completely puts the controller down on a table. The player should rightfully expect that his or her character in game will not move around. However, if the issue isn't handled, the game will detect some value of input to the axis and move the character.

Furthermore, many games have the character move based on how far the analog stick is moved in one direction—so that slightly moving the stick might cause the character to slowly walk, whereas moving the stick all the way in a direction might cause the character to sprint. However, if you only make the player sprint when the axis reports the maximum value, the player will never sprint.

To solve this issue, code that processes the input from an axis should **filter** the value. Specifically, you want to interpret values close to zero as zero and values close to the minimum or maximum as the minimum or maximum. Furthermore, it's convenient for users of the input system if you convert the integral ranges into a normalized floating-point range. For the axes that yield both positive and negative values, this means a range between −1.0 and 1.0.

Figure 8.2 shows an example of such a filter for a single axis. The numbers above the line are the integral values before filtering, and the numbers below the line are the floating-point values after filtering. The area near zero that you interpreted as 0.0 is called a **dead zone**.

![](img/e9afcec1487716b0ef80d7e7c09869c8_579_0.png)

**Figure 8.2** A sample filter for an axis, with the input values above and the output values below

Listing 8.7 shows the implementation of the `InputSystem::Filter1D` function, which the input system uses to filter one-dimensional axes such as the triggers. First, you declare two constants for the dead zone and maximum value. Note that `deadZone` here is `250`—which is less than in **Figure 8.2** because this value works better for the triggers (but you could make the constants parameters or user configurable, if desired).

Next, the code takes the absolute value of the input by using a ternary operator. If this value is less than the dead zone constant, you simply return `0.0f`. Otherwise, you convert the input to a fractional value representing where it lands in between the dead zone and the maximum value. For example, an input halfway between deadZone and maxValue is 0.5f.

Then you ensure that the sign of this fractional value matches the sign of the original input. Finally, you clamp the value to the range of -1.0 to 1.0 to account for the cases where the input is greater than the maximum value constant. The implementation Math::Clamp is in the custom Math.h header file.

### Listing 8.7 Filter1D Implementation

Click here to view code image

```
float InputSystem::Filter1D(int input)
{
    // A value < dead zone is interpreted as 0%
    const int deadZone = 250;
    // A value > max value is interpreted as 100%
    const int maxValue = 30000;
    float retVal = 0.0f;
    // Take absolute value of input
    int absValue = input > 0 ? input : -input;
    // Ignore input within dead zone
    if (absValue > deadZone)
    {
        // Compute fractional value between dead zone and max
        retVal = static_cast<float>(absValue - deadZone) / (maxValue - deadZone);

        // Make sure sign matches original value
        retVal = input > 0 ? retVal : -1.0f * retVal;

        // Clamp between -1.0f and 1.0f
        retVal = Math::Clamp(retVal, -1.0f, 1.0f);
    }

    return retVal;
}
```

Using the `Filter1D` function, an input value of 5000 returns 0.0f, and a value of -19000 returns -0.5f.

The `Filter1D` function works well when you only need a single axis, such as for one of the triggers. However, because the analog sticks really are two different axes in concert, it's usually preferable to instead filter them in two dimensions, as discussed in the next section.

For now, you can add two floats to `ControllerState` for the left and right triggers:

```
float mLeftTrigger;
float mRightTrigger;
```

Next, in `InputSystem::Update` use the `SDL_GameControllerGetAxis` function to read in the values of both triggers and call the `Filter1D` function on this value to convert it to a range of 0.0 to 1.0 (because triggers cannot be negative). For example, the following sets the `mLeftTrigger` member:

Click here to view code image

```
mState.Controller.mLeftTrigger =
    Filter1D(SDL_GameControllerGetAxis(mController,
        SDL_CONTROLLER_AXIS_TRIGGERLEFT));
```

You then add `GetLeftTrigger()` and `GetRightTrigger()` functions to access these. For example, the following code gets the value of the left trigger:

Click here to view code image

```
float left = state.Controller.GetLeftTrigger();
```

## Filtering Analog Sticks in Two Dimensions

A common control scheme for an analog stick is that the orientation of the stick corresponds to the direction in which the player's character moves. For example, pressing the stick up and to the left would cause the character onscreen to also move in that direction. To implement this, you should interpret the x- and y-axes together.

Although it is tempting to apply the Filter1D function to the x- and y-axes independently, doing so can cause an interesting issue. If the player moves the stick all the way up, interpreting it as a normalized vector yields <0.0, 1.0>. On the other hand, if the player moves the stick all the way up and to the right, the normalized vector is <1.0, 1.0>. The length of these two vectors is different, which is a problem if you use the length to dictate the speed at which the character moves: The character could move faster diagonally than straight in one direction!

Although you could just normalize vectors with a length greater than one, interpreting each axis independently still ultimately means you're interpreting the dead zone and maximum values as a square. A better approach is to interpret them as concentric circles, as shown in Figure 8.3. The square border represents the raw input values, the inner circle represents the dead zone, and the outer circle represents the maximum values.

![](img/e9afcec1487716b0ef80d7e7c09869c8_584_0.png)

Figure 8.3 Filtering in two dimensions

Listing 8.8 gives the code for Filter2D, which takes in both the x- and y-axes for the analog stick and filters in two dimensions. You first create a 2D vector and then determine the length of that vector. Lengths less than the dead zone result in Vector2::Zero. For lengths greater than the dead zone, you determine the fractional value between the dead zone and max and set the length of the vector to this fractional value.

### Listing 8.8 InputSystem::Filter2D Implementation

Click here to view code image

```
Vector2 InputSystem::Filter2D(int inputX, int inputY)
{
    const float deadZone = 8000.0f;
    const float maxValue = 30000.0f;

    // Make into 2D vector
    Vector2 dir;

    dir.x = static_cast<float>(inputX);
    dir.y = static_cast<float>(inputY);

    float length = dir.Length();

    // If length < deadZone, should be no input
    if (length < deadZone)
    {
        dir = Vector2::Zero;
    }

    else
    {
        // Calculate fractional value between
        // dead zone and max value circles

        float f = (length - deadZone) / (maxValue - deadZone);

        // Clamp f between 0.0f and 1.0f
        f = Math::Clamp(f, 0.0f, 1.0f);
        // Normalize the vector, and then scale it to the
        // fractional value
        dir *= f / length;
    }
    return dir;
}
```

Next, add two Vector2s to ControllerState for the left and right sticks, respectively. You can then add code in InputSystem::Update to grab the values of the two axes for each stick and then run Filter2D to get the final analog stick value. For example, the following code filters the left stick and saves the result in the controller state:

Click here to view code image

```
x = SDL_GameControllerGetAxis(mController,
SDL_CONTROLLER_AXIS_LEFTX);
y = -SDL_GameControllerGetAxis(mController,
SDL_CONTROLLER_AXIS_LEFTY);
```

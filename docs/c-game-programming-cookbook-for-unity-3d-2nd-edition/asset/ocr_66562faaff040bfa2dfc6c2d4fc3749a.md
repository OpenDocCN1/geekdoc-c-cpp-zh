Code from this script will eventually interpolate heights and rotation values, but it requires a little extra before we can do that:

```
wantedHeight = _cameraTarget.position.y + height;
currentHeight = _TR.position.y;

wantedRotationAngle = _cameraTarget.eulerAngles.y;
currentRotationAngle = _TR.eulerAngles.y;
```

Before interpolation, we need to calculate target height and target rotations and we also need to find out what current height and rotation values are. The public variable height – which is our value set in the Inspector to tell this script how high to put the camera – gets added to wantedHeight along with the height of the target object we are following. With this new float value in wantedHeight, we now know exactly where the camera needs to be headed height-wise.

currentRotationAngle is a float representing the angle, in degrees, that we need to turn the camera at to try and reach the target rotation in wantedRotationAngle. It's an interpolation carried out by Mathf.SmoothDampAngle in the next line:

```
currentRotationAngle = Mathf.SmoothDampAngle(currentRotationAngle, wantedRotationAngle, ref yVelocity, rotationSnapTime);
```

Mathf.SmoothDampAngle is an interpolation function designed specifically for easing between two angles. It will automatically cap the return value between 0 and 360 as well as choosing the correct way around (if your value is at 181 degrees, it would interpolate up rather than down so that the rotation has a natural flow and doesn't go back on itself).

The Unity documentation tells us that SmoothDampAngle takes the following parameters (in order of how they should be passed in):

| current | The current position. |
| target | A Vector3 position we are trying to reach. |
| currentVelocity | The current velocity, this value is modified by the function every time you call it. |
| smoothTime | Approximately the time it will take to reach the target. A smaller value will reach the target faster. |
| maxSpeed | Optionally allows you to clamp the maximum speed. |
| deltaTime | Time since the last call to this function. Default is Time.deltaTime. |

In this part of the code, the yVelocity variable holds the current velocity of the interpolated move, but it is not actually used anywhere else in the script. It's a required field for SmoothDampAngle, so we just provide it for the function to work right and forget about it. Note that one possible use for getting the velocity may be speed limiting the move, but SmoothDampAngle can take care of this with no extra code by providing a maxSpeed parameter. This is useful for limiting interpolation speeds without having to do it yourself with velocity. The currentRotationAngle is, in effect, a portion of the rotation we need to make around the y-axis (hence using the name yVelocity to describe its speed). The variable rotationSnapTime decides how much time it should take for the rotation to happen, which is public and designed to be set in the Unity editor Inspector window on whichever GameObject the script is attached to, so that the rotation speed can be easily set in the editor. Height is interpolated using Mathf.Lerp, which takes three parameters: the start amount, the target amount, and a time value clamped between 0 and 1.
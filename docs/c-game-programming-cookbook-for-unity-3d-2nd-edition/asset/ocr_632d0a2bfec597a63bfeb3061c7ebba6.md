We use the float heightDamping, multiplied by Time.deltaTime, to make the transition time based. Wondering why do we need to make the time parameter time based? Good question! How the time parameter of Mathf.Lerp works has been a very popular question on various forums and help pages. The time value represents how much of a portion, of the difference between the two values, that should be applied each time this line of code is executed. If the time value is zero, the return value will be the start amount. If time is 1, the return value will be the target amount.

By calculating the portion with Time.deltaTime, the transition from start value to target value is smoothed out over a repeatable, fixed amount of time rather than it being frame-rate dependent and based on how many times the Mathf.Lerp calculation line is called:

```
currentHeight = Mathf.Lerp(currentHeight,
 wantedHeight, heightDamping * Time.deltaTime);
```

Now that the script has calculated how much to rotate the camera and how high it should be on the y-axis, the script goes on to deal with positioning: wantedPosition is a Vector3 that will hold the target position. The target position is made from the target Transform.position followed by setting its y position to the height calculated earlier in this section in currentHeight variable:

```
wantedPosition = target.position;
 wantedPosition.y = currentHeight;
```

The next part of the code calculates how far behind the player we need to move the camera. For this, the script uses Mathf.SmoothDampAngle. zVelocity represents the speed of movement of the camera along its z-axis:

```
usedDistance = Mathf.SmoothDampAngle(usedDistance,
 distance, ref zVelocity, distanceSnapTime);
```

To place the camera at the correct position around the target using only a rotation angle, the solution lies within Quaternion.Euler. This rather frightening sounding function converts Euler angle vector3-based rotations into a vector. That is; you pass in Euler rotation values and you get back a direction vector instead. Multiply this by how far back we want the camera from the player; add that to the player's current position and we have the correct rotation, position and offset for the camera:

```
wantedPosition += Quaternion.Euler(
 currentRotationAngle, 0) * new Vector3(0, 0, -usedDistance);
 _TR.position = wantedPosition;
```

The final part of the function causes the camera to look at the target (player). It does this by using Unity's built-in Transform.LookAt() function. We pass in the position of the target object (as a Vector3) and add an extra offset to where the camera is going to look, via the lookAtAdjustVector variable. Note that you can also add an up vector to the LookAt() function, but in this case, we don't need to:

```
_TR.LookAt(_cameraTarget.position);
 _TR.Rotate(lookAtAdjustVector);
```

Above, in the last line we also add a small rotation adjustment. I like to use this so that the camera aims above the player as if it were looking forward, rather than looking right at the players vehicle or body. This can make the camera view
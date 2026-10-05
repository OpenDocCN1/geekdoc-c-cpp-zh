Directional movements use the world x- and z-axes to decide which way to move; that is, the player moves along the world x or z axis based on the button pressed by the player. UpdateDirectionalMovement() function starts by taking the horizontal and vertical input (from the horizontal and vert) and multiplying them by the world forward vector or the world right vector, respectively. Note that the targetDirection variable is of Vector3 type and it starts being set to the horizontal direction and then has the vertical added to it, encompassing both vertical and horizontal movement into the same vector:

```
void UpdateDirectionalMovement() {
    // find target direction
    targetDirection= horiz * Vector3.right;
    targetDirection+= vert * Vector3.forward;
}
```

As the code comments tell you, we store speed and direction separately. By so, we can have the character face a particular direction without actually moving, a behavior sometimes for this type of game.
TheargetDirection variable will be zero when there is no user input, so before calculating any movement amounts, that movement is intended first:

```
// store speed and direction
// so that when the character stands still we still have a
// valid forward direction
// moveDirection is always normalized, and we only update it
// if there is user input
if (targetDirection != Vector3.zero) {
```

The moveDirection vector will be used to move the player around the arena. Its comes from an interpolation between the current value of moveDirection and the targetDirection calculated earlier from the user inputs. This vector is multiplied by rotateSpeed, converted into radians, and again multiplied by Time.deltaTime to make the rotation speed based. This ensures that the rotation ends in the specified position.
The Unity documentation describes Vector3.RotateTowards as follows:
This function is similar to MoveTowards except that the vector is treated as a direction rather than a position. The current vector will be rotated round the target direction by an angle of maxRadiansDelta, although it will land exactly on the target rather overshoot. If the magnitudes of current and target are different then the magnitude of the result will be interpolated during the rotation. If a negative value is used for maxRadiansDelta, the vector will rotate away from target until it is in exactly the opposite direction, then stop.

The moveDirection vector is then normalized to remove any magnitude from the equation:

```
moveDirection = Vector3.RotateTowards(moveDirection,
targetDirection, rotateSpeed * Mathf.Deg2Rad * Time,
deltaTime, 1000);
moveDirection = moveDirection.normalized;
```
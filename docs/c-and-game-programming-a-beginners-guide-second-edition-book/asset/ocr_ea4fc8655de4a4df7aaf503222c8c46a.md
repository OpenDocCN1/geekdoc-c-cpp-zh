```
imagePosX = constraintBox.X +
    constraintBox.Width - imageWidth;
    retVal = true;
}

if (imagePosY < constraintBox.Y) {
    imagePosY = constraintBox.Y;
    retVal = true;
} else if (((imagePosY + imageHeight) >
(constraintBox.Y + constraintBox.Height)) {
    imagePosY = constraintBox.Y +
        constraintBox.Height - imageHeight;
    retVal = true;
}

return retVal;
}
```

As with ConstrainToBox, Deflect limits our character's movement. In this case, however, the character's direction is reversed, forcing our player to move in the opposite direction. The player feels bumped back as he continues to manipulate the controls in the direction he desires.

# Example 5.66. Deflect.

```
// Basic deflection
// Returns whether any position changes were made.
virtual public bool Deflect(int x, int y, int width, int height) {
    if (!isActive)
        return false;

    switch(direction) {
    case SOUTHWEST:
        if (imagePosX <= x) {
            direction = SOUTHEAST;
        } else {
            direction = NORTHWEST;
        }
        break;
    case SOUTH:
        direction = NORTH;
        break;
```
```
targets[i].imagePosX > player.imagePosX - 50) {
    FireBomb(i);
    . . .
```

# Defining Character Limitation

Preventing characters from moving off the screen is just a matter of practicality. Theoretically, the game could be played off the screen, but this would make little sense. Also, since there are limits to the range of our characters' values, it is foreseeable that if a character was left to run amuck, it could exceed those values and cause an error (see Examples 4.46 and 4.47).

# Example 4.46. Character limits (from AnimatedImage.cs).

```
```csharp
// Moves the image to be within the specified boundary.
// Returns whether any position changes were made.
virtual public bool ConstrainToBox() {
    bool retVal = false;

    if (!isActive)
        return false;

    if (imagePosX < constraintBox.X) {
        imagePosX = constraintBox.X;
        retVal = true;
    } else if ((imagePosX + imageWidth) >
        (constraintBox.X + constraintBox.Width)) {
        imagePosX = constraintBox.X +
            constraintBox.Width - imageWidth;
        retVal = true;
    }

    if (imagePosY < constraintBox.Y) {
        imagePosY = constraintBox.Y;
        retVal = true;
    } else if ((imagePosY + imageHeight) >
        (constraintBox.Y + constraintBox.Height)) {
        imagePosY = constraintBox.Y +
            constraintBox.Height - imageHeight;
        retVal = true;
    }
}
```
```
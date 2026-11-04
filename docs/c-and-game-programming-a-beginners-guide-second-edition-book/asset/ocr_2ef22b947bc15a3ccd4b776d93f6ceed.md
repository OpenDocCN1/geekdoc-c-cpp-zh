```
case SOUTHEAST:
    if ((imagePosX + imageWidth) >= (x + width)) {
        direction = SOUTHWEST;
    } else {
        direction = NORTHEAST;
    }
    break;
case WEST:
    direction = EAST;
    break;
case EAST:
    direction = WEST;
    break;
case NORTHWEST:
    if (imagePosY <= y) {
        direction = SOUTHWEST;
    } else {
        direction = NORTHEAST;
    }
    break;
case NORTH:
    direction = SOUTH;
    break;
case NORTHEAST:
    if (imagePosY <= y) {
        direction = SOUTHEAST;
    } else {
        direction = NORTHWEST;
    }
    break;
}
return true;

// Deflect override -- deflects off of a given AnimatedImage
virtual public bool Deflect(AnimatedImage img) {
    return Deflect(img.imagePosX, img.imagePosY,
        img.imageWidth, img.imageHeight);
}

// Deflect override -- deflects off of default constraint box
virtual public bool Deflect() {
    return Deflect(constraintBox.X, constraintBox.Y,
        constraintBox.Width, constraintBox.Height);
}
```
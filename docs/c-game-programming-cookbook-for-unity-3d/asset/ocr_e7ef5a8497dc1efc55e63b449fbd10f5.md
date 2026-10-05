```
prevMousePos = Input.mousePosition;
```

```
}
```

The input scripts use CheckInput() as their default main update function, is intended to be called from the player class.

The mouse input system uses mouse delta movement (the amount of movement since the last update) instead of mouse position. The delta amount is converted into a percent-age (a percentage of a screen width or height), and the resulting value is used as input.

CheckInput() starts by calculating a value to work at. The floats scalerX and scalerY hold the equivalent of 1% of the screen's width and height, respectively:

```
public override void CheckInput()
    // get input data from vertical and horizontal axis and
    // store them internally in vert and horz so we don't
    // have to access them every time we need to relay input
    // data out

    // calculate a percentage amount to use per pixel
    float scalerX = 100f / Screen.width;
    float scalerY = 100f / Screen.height;
```

The delta amount of mouse movement is calculated in the code by taking the current mouse position and subtracting it from the position that the mouse was at the end of the last update.

```
// calculate and use deltas
float mouseDeltaY = Input.mousePosition.y - prevMousePos.y;
float mouseDeltaX = Input.mousePosition.x - prevMousePos.x;
```

When the mouse position is multiplied by the scale variables (scalerX and scalerY), we end up with a percentage amount. We say that the mouse is at a percentage amount across the screen and use that percentage amount as:

```
// scale based on screen size
vert += (mouseDeltaY * speedY) * scalerY;
horiz += (mouseDeltaX * speedX) * scalerX;
```

```
// store this mouse position for the next time we're here
prevMousePos = Input.mousePosition;
```

The mouse-based input scripts also populate Boolean variables for directional-ment, if required:

```
// set up some Boolean values for up, down, left and right
Up = (vert > 0);
Down = (vert < 0);
Left = (horz < 0);
Right = (horz > 0);
```

To make the fire button work properly, mouse button must be set up correctly in the input settings of the Unity editor, under the Fire entry:

# 4.7 Input Scripts
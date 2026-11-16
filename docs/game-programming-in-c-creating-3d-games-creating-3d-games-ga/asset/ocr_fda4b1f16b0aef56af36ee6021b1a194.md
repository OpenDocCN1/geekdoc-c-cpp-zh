in GenerateOutput—after clearing the back buffer
but before swapping the front and back buffers.

For drawing filled rectangles, SDL has a
SDL_RenderFillRect function. This function takes in
an SDL_Rect that represents the bounds of the rectangle
and draws a filled-in rectangle using the current draw
color. Of course, if you keep the draw color the same as
the background, you won’t see any rectangles. You
therefore need to change the draw color to white:

Click here to view code image

```
SDL_SetRenderDrawColor(mRenderer, 255, 255, 255, 255)
```

Next, to draw the rectangle, you need to specify
dimensions via an SDL_Rect struct. The rectangle has
four parameters: the x/y coordinates of the top-left
corner of the rectangle onscreen, and the width/height of
the rectangle. Keep in mind that in SDL rendering, as in
many other 2D graphics libraries, the top-left corner of
the screen is (0, 0), positive x is to the right, and positive
y is down.

For example, if you want to draw a rectangle at the top of
the screen, you can use the following declaration of an
SDL_Rect:

```
SDL_Rect wall{
    0,    // Top left x
```
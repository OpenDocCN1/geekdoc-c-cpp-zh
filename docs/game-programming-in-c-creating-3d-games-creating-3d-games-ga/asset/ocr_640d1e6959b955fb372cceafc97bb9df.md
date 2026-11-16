```
}
```

Here, you update the y position of the paddle based on the paddle direction, a speed of 300.0f pixels/second, and delta time. If mPaddleDir is -1, the paddle will move up, and if it's 1, it'll move down.

One problem is that this code allows the paddle to move off the screen. To fix this, you can add boundary conditions for the paddle's y position. If the position is too high or too low, move it back to a valid position:

# Click here to view code image

```
if (mPaddleDir != 0)
{
    mPaddlePos.y += mPaddleDir * 300.0f * deltaTime;
    // Make sure paddle doesn't move off screen!
    if (mPaddlePos.y < (paddleH/2.0f + thickness))
    {
        mPaddlePos.y = paddleH/2.0f + thickness;
    }
    else if (mPaddlePos.y > (768.0f - paddleH/2.0f - t
    {
        mPaddlePos.y = 768.0f - paddleH/2.0f - thicknes
```
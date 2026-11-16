game would be over in a heartbeat!

To solve this issue, games use **delta time**: the amount of elapsed game time since the last frame. To convert the preceding code to using delta time, instead of thinking of movement as pixels per frame, you should think of it as pixels per second. So, if the ideal movement speed is 150 pixels per second, the following code is much more flexible:

# Click here to view code image

```
// Update x position by 150 pixels/second

enemy.mPosition.x += 150 * deltaTime;
```

Now the code will work well regardless of the frame rate. At 30 FPS, the delta time is ~0.033, so the enemy will move 5 pixels per frame, for a total of 150 pixels per second. At 60 FPS, the enemy will move only 2.5 pixels per frame but will still move a total of 150 pixels per second. The movement certainly will be smoother in the 60 FPS case, but the overall per-second speed remains the same.

Because this works across many frame rates, as a rule of thumb, everything in the game world should update as a function of delta time.

To help calculate delta time, SDL provides an `SDL_GetTicks` member function that returns the number of milliseconds elapsed since the `SDL_Init`
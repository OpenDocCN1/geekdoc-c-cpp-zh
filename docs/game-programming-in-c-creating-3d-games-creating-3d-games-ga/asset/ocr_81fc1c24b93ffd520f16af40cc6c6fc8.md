state of the spacebar. Suppose the spacebar is up for the first three frames, and then the player presses the spacebar prior to frame 4. The player continues to hold the spacebar down until prior to frame 6 and then releases it. You can draw this as a graph, as in Figure 8.1, where the x-axis corresponds to the time at each frame and the y-axis corresponds to the binary value for that frame. On frame 4, the spacebar changes from 0 to 1, and on frame 6, the spacebar changes back from 1 to 0. The frame where the input changes from 0 to 1 is a **positive edge** (or rising edge), and the frame where the input changes from 1 to 0 is a **negative edge** (or falling edge).

![](bbox=[0.16, 0.46, 0.73, 0.71])

Figure 8.1 Graph of the spacebar polled over nine frames

Now consider what would happen if the process input for the character simply said the following (in pseudocode):

```
if ( spacebar == 1 )
```
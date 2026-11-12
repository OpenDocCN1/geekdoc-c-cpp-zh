(entities).
It gives us the ability to see how well our engine performs when it has to render many entities. Check your task manager to see how much of the CPU and the GPU is used.

![](bbox=[0.08, 0.14, 0.92, 0.4])

Figure 32 Turning Texture to Tile Map

The picture above shows the result we get from the tile map renderer. It looks like we’ve just rendered the texture, but the grid actually shows the individual tiles.
We could say this is the most inefficient way to render a texture ■■.
The advantage that comes with having each tile an entity is that we can add another component to the tiles to give them more functionalities than just being seen on the screen. We could for example add a destructible component to some tiles to make them destructible or maybe attach an event to it so that some action can be executed when the player collides with it. It’s just a matter of imagination.
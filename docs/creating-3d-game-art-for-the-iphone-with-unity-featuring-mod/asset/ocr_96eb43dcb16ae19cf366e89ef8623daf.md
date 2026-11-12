![](bbox=[0.12, 0.105, 0.97, 0.59])

FIG 4.4 The Level Can Be Broken Down into Smaller Tileable Elements.

For instance, you could setup a blockade, which controls how much the player is aloud to backtrack in a level. Once the player has reached a certain position, you can safely unload the section. Now, discussing the implementation of this procedure is beyond the scope of this book, but it's important to understand the advantages to breaking the level down into sections in terms of loading. For this method, each section is saved as a separate FBX file that can be loaded when needed. Also, with each section exported as a separate file, you can implement an asset downloading mechanism to your game so that player can use In-App purchases.

# ### Optimize Batching and Rendering

As we discussed in Chapter 1, batching is extremely important for optimizing your game's performance, and special care needs to be taken to make sure that your meshes can and will be able to batch. By breaking the level into sections, you gain two advantages in terms of rendering vertices. First, it will be easier to stay within the 300-vertex limit that is a restriction of Dynamic
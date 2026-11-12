![](bbox=[0.11, 0.108, 0.951, 0.428])

*FIG 2.1 Here You Can See Tater and Thumper, the Main Assets We'll Be Focusing on Throughout This Chapter.*

# ## Planning the Vertex Budget

**Tater's Weapon Load Out**

Go to the resource site to view the video walkthrough for this chapter.

We talked a lot in Chapter 1, “Getting to Know the iDevice Hardware and Unity iOS,” about the game budget. Part of working out a game budget is to come up with a budget for the amount of vertices your models will be made up of. The vertex budget is the process of deciding exactly how many vertices the objects that make up your scene contain and is shown per frame of the game loop, while still maintaining your game budget's frame rate. This is key to the modeling process because you can't model anything without knowing the limitations of the targeted device, your game's target frame rate and your overall vertex budget. You need to have a vertex count worked out before a single polygon is created in your 3D application. In Chapter 1, “Getting to Know the iDevice Hardware and Unity iOS,” we filled in the first piece of this puzzle by discussing the various hardware components found in the different iDevices in order to gain an understanding of its limitations and thus establish a baseline to follow in order to create optimized geometry for the iPhone and iPad. In the next section, we'll take a look at how you can go about determining your vertex budget.

# ## Testing Performance

So we've determined that planning the vertex budget is the first step before creating any actual geometry, but how is this budget actually determined? In game development, you'll hear the phrase, “it depends” quite often. Although it may sound like a quick answer to a complicated question, however, it's actually the truth. Determining a vertex budget or any budget in game development depends solely on your game. The type of game you're
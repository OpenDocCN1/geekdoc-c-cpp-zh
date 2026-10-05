# Unity Games by Tutorials

# Chapter 9: The Player and Environment

![](bbox=[0.303, 0.087, 0.696, 0.323])

Click Play and test your weapons, switching between them with 1, 2 or 3.

![](bbox=[0.318, 0.365, 0.681, 0.533])

# Adding the reticle

It's time to add the reticle each gun will use. The reticle is just a simple 2D image placed in front of the camera. It is the equivalent of pasting a layer over the lens of your cell phone camera! It's not very technical, but it gets the job done.

You'll be using Unity's user interface tools. In a few more chapters, you'll really learn about them in depth. For this chapter, consider this section a warm-up!

To started placing user interface elements you need a canvas. Unity provides several types of canvases. For this game, you'll use an overlay canvas. This works as an overlay on top of the screen. Elements added to the overlay will cover the game behind it, but you can minimize the effect through transparency.

In the Hierarchy, click Create and select UI Canvas and rename the created GameObject to GameUI. Right-click on the GameUI GameObject, select UI ► Image and rename the Image to Reticle.

raywenderlich.com

258
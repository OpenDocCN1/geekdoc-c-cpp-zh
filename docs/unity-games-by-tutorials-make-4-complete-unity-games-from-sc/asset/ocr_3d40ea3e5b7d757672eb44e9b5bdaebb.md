Unity has a Resources class that lets you access assets in your project via code — any assets placed in a sub-folder of the Assets folder bears the name Resources can be accessed via Resources.Load() methods.

You're exploring the Resources class now because you'll create your own code for saving and loading that'll let you save a new level to a JSON file. This file will keep references to items used to create the level, e.g., blocks and hazards.

It's impractical to add public fields for every prefab used in a level. The JSON file will call the Resources.Load() methods to find the referenced objects by name.

Create a folder called Resources in the Assets folder. Then create a sub-folder inside named Prefabs. Now you'll create the first few prefabs.

One at a time, drag the single-block, top-left-corner-small, Buzzaw, and SoyBoy GameObject from the Hierarchy, and then drop them into the Prefabs folder.

![](bbox=[0.239, 0.383, 0.759, 0.477])

Unity will allow resource items in game builds, whether they end up used or not. It's important to know because they can sneakily increase your build size.

# Scripting basic controls

You're nearing the end of this chapter! But before you get there, you need to dive into scripting so you can implement Super Soy Boy's animations. He's dying to show you just how nimble a little tofu chunk can be!

Scripting isn't hard, but it's good to ease into when you're learning. As such, you'll start with some validation for the GameObject, then layer in more script to get him facing the right direction, and then you'll get him.

Hold on there... does he have any ground to run on? Not last time you checked. Remember that you had to enable the Kinematic Body type to preview his animation? Before you write one line of code, you need to give Super Soy Boy some stable footing.

In the Scene view, make seven clones of the single-block GameObject prefab and set them next to each other in a line.
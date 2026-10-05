# Imported animations

Unity provides a number of tools for animating GameObjects, and as you know, you've already imported some with the space marine and alien! All you need to do is incorporate them into your game, which is pretty easy.

In the Project view, select the BobbleEnemy-Body GameObject from the Models folder. You'll see four tabs in the Inspector: Model, Rig, Animation and Materials.

![](bbox=[0.268, 0.279, 0.732, 0.463])

The Materials tab, new with Unity 2018.1, deals with textures that are imported with your model. The Model and Rig tabs deal with the actual model structure.

# Avatars and Rigs

Typically, models are rigged, which means Unity creates a system that acts as a virtual skeleton to help your models naturally.

For instance, when you move an arm of a model, all the child GameObjects that comprise the arm move in accordance with the rig's limitations, as well as that you dictate.

Rigs in Unity are called avatars and they can share animations. Unity provides a library of free motion capture animations and, with a proper rig, you can incorporate these motions with minimal work.

The Animations tab is where you configure your imported animations. You're about to get a crash course in all this... starting now!

# Animating the alien

Click the Animation tab. Here are the animations you imported with the model.
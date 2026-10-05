+   Move to Front and Move to Back adjust the ordering of sprites in 2D games.

+   Remove Component will delete the component from the GameObject — you can undo this action.

+   Copy Component allows you to copy a component from one GameObject and paste it onto another.

+   Paste Component as New will paste a copied component to a GameObject.

Paste Component Values allows you to overwrite the values of the current component from a copied component. Specifically, you can copy the values of a component while your game is being played. When you stop the game, you can paste those values onto another component. This is quite useful because sometimes it's useful to tweak things as you play to see what works in practice.

From the menu, select remove component. Now click the add component button again, and add a Rigidbody back to the GameObject. It's in the Physics category. Finally, click the presets and select the Kinematic preset.

Notice that the Rigidbody component was auto-magically updated by your preset. But you may be asking, what's a Rigidbody?

By adding the Rigidbody component to the space marine, you've made it so that he can respond to collision events and to gravity. However, you don't want him bouncing off enemies or walls. You definitely want to know about those collisions events, but you don't want the hero to fly out of control just because he bumped into a column.

The kinematic property tells the physics engine that you are manually controlling the marine, rather than letting the physics engine move the marine for you. But the physics engine is still aware of when the marine collides with an alien, and when it collides with something. This engine will notify you so you can make something happen — like the space marine getting chomped!

By unchecking the Gravity option, the space marine won't be affected by gravity. Again — you don't need this because you'll be moving the marine manually and are using the Rigidbody for collision detection.

Now comes the fun part: It's time to make that marine dance! Or move. That's fine, too.

Unity provides some built-in components to make movement easy, and you'll use them in Chapter 4, "Physics." But for learning purposes, in this chapter, you'll do everything manually through the power of scripting.

![](bbox=[0.121, 0.933, 0.285, 0.955])
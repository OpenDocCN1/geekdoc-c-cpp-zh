Open the Animator editor — find it under Window > Animation > Animator from the top menu — and select the SoyBoy GameObject in the Hierarchy. This will display the layout of the SoyBoy.controller you'll hook up the animation states, but not yet.

Notice how the four clips are, as well as a default Entry state that moves straight onto the RunAnimation clip.

![](bbox=[0.199, 0.23, 0.8, 0.375])

I know you're eager to preview but, first, select SoyBoy and temporarily select Kinematic on the Rigid 2d component for Body Type. If you don't do this, then gravity will drop that little chunk of tofu into the infinite editor void when the game starts!

Play the game in the editor so you can see how Super Soy Boy runs the moment the game starts. Somebody wants noodles!

Re-select Dynamic for Body Type on the Rigidbody after previewing the animation.

> Note: In Chapter 13, "More Unity 2D," you'll link these three animation states and write code to transition between them based on the player's actions.

# Layers and sorting

When arranging sprites on screen in a 2D environment, you don't work with a z-axis like you do in 3D. Instead, you think in terms of Sorting Layers and Order in Layer.

Think of this concept as pieces of glass stacked atop each other with sprites between each layer. You're viewing the stack from the top, so what's visible and hidden depends on the stack order.
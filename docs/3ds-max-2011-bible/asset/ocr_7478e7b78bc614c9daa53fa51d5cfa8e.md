# Using Animation Layers, Modifiers, and Complex Controllers

Just as layers can be used to organize a scene by placing unique objects on different layers, you also can separate the various animation motions into different layers. This gives you great control over how motions are organized and blended together.

If you’ve worked to animate some Max object and are pleased with the result, you can save the animation clip and reuse it. Several animation clips can be mixed together to create an entirely new animation sequence.

Modifiers can be used to deform and otherwise alter the geometry of objects, but they also can be used to affect other aspects of an object, including animated changes. One such important animation modifier is the Point Cache modifier. This modifier lets the movement of each vertex in the scene be saved to a cached file for immediate recall and for animating multiple objects simultaneously.

The Modifiers menu also includes an Animation submenu that contains many such modifiers. These modifiers are unique in that each of them changes with time. They can be useful as an alternate to controllers, but their resulting effects are very specific. Included with this submenu are modifiers such as Morpher, which allows an object to move through several different preset shapes, and Flex, which is used to add soft-body dynamics to your scene. Other animation modifiers include Melt and PathDeform.

This chapter also discusses all those miscellaneous Controllers that weren’t covered earlier. These Controllers are more complex and enable a wide range of unique motions.

# IN THIS CHAPTER

+   - Using animation layers
+   - Saving and loading animation files
+   - Using the Point Cache modifier
+   - Using the Morpher modifier
+   - Adding secondary animation with the Flex modifier
+   - Animating geometry deformations
+   - Using other animation modifiers
+   - Examining controllers

# Using the Animation Layers Toolbar

Behind the scenes, animation layers add several new controller tracks to objects that are visible in the Motion panel and in the Track View interface, but the front end is accessible through a simple toolbar. The Animation Layers toolbar, shown in Figure 34.1, is similar in many ways to the Layers toolbar.
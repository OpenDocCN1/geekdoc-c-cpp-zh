
draw a different texture. For a radar, you can project the player and any enemy objects onto the x/y plane and use these converted coordinates to determine where to draw a blip on the radar.

Finally, the UI needs code to handle text for different locales. A simple map can convert between text keys and values. Using UTF-8 encoding of these text values makes it relatively painless to use. The RapidJSON library can load in JSON files encoded in UTF-8, and SDL TTF supports rendering UTF-8 strings.

## ADDITIONAL READING

Desi Quintans’ short article gives examples of good and bad game UI, from a design perspective. Luis Sempé, a UI programmer for games including Deus Ex: Human Revolution, has written the only book solely dedicated to programming UIs for games. (In the interest of full disclosure, I worked with the author many years ago.) Finally, Joel Spolsky’s book is for UI design in general, but it provides insight into how to create an effective UI.

- Quintans, Desi. “Game UI by Example: A Crash Course in the Good and the Bad.” https://gamedevelopment.tutsplus.com/tutorials/game-ui-by-example-a-crash-course-in-the-good-and-the-bad--gamedev-3943. Accessed September 10, 2017.
- Sempé, Luis. User Interface Programming for Games. Self-published, 2014.
- Spolsky, Joel. User Interface Design for Programmers. Berkeley: Apress, 2001.

## EXERCISES

In this chapter's exercises, you explore adding a main menu as well as making changes to the game's HUD.

### Exercise 11.1

Create a main menu. To support this, the game class needs a new state called EMainMenu. The game should first start in this state and display a UI screen with the menu options Start and Quit. If the player clicks Start, the game should switch to gameplay. If the player clicks Quit, the menu should show a dialog box confirming that the player wants to quit.

To add further functionality, consider spawning the actors only when first entering the gameplay state from the main menu. In addition, change the pause menu so that the Quit option deletes all actors and returns to the main menu rather than immediately quitting the game.

### Exercise 11.2

Modify the radar so that it uses different blip textures, depending on whether the actor is above or below the player. Use the provided BlipUp.png and BlipDown.png textures to show these different states. Testing this feature may require changing the positions of some of the target actors in order to more clearly distinguish the height.

### Exercise 11.3

Implement an onscreen 2D arrow that points to a specific actor. Create a new type of actor called ArrowTarget and place it somewhere in the game world. Then, in the HUD, compute the vector from the player to the ArrowTarget. Use the angle between this and the player's forward on the x-y plane to determine the angle to rotate the onscreen 2D arrow. Finally, add code to UIScreen::DrawTexture to supporting rotating a texture (with a rotation matrix).

## CHAPTER 12

### SKELETAL ANIMATION

Animating characters for a 3D game is very different from animating characters for a 2D game. This chapter looks at *skeletal animation*, the most common animation used in 3D games. This chapter first goes over the mathematical foundations of the approach and then dives into the implementation details.

### FOUNDATIONS OF SKELETAL ANIMATION

As described in Chapter 2, “Game Objects and 2D Graphics,” for 2D animation, games use a sequence of image files to yield the illusion of an animated character. A naïve solution for animating 3D characters is similar: Construct a sequence of 3D models and render those different models in rapid succession. Although this solution conceptually works, it’s not a very practical approach.

Consider a character model composed of 15,000 triangles, which is a conservative number for a modern game. Assuming only 10 bytes per vertex, the total memory usage of this one model might be around 50 to 100 KB. A two-second animation running at 30 frames per second would need a total of 60 different models. This means the total memory usage for this single animation would be 3 to 6 MB. Now imagine that the game uses several different animations and several different character models. The memory usage for the game’s models and animations will quickly become too high.

In addition, if a game has 20 different humanoid characters, chances are their movements during an animation such as running are largely the same. If you use the naïve solution just described, each of these 20 characters needs a different model set for its animations. This also means that artists need to manually author these different model sets and animations for each character.

Because of these issues, most 3D games instead take inspiration from anatomy: vertebrates, like humans, have bones. Attached to these bones are muscles, skin, and other tissue. Bones are rigid, while the other tissues are not. Thus, given the position of a bone, it's possible to derive the position of the tissue attached to the bone.

Similarly, in **skeletal animation**, the character has an underlying rigid skeleton. This skeleton is what the animator animates. Then, each vertex in the model has an association with one or more bones in the skeleton. When the animation moves the bones, the vertices deform around the associated bones (much the way your skin stretches when you move around). This means that there only needs to be a single 3D model for a character, regardless of the number of animations for the model.

> note
> Because skeletal animation has bones and vertices that deform along the bones, some call this technique **skinned animation**. The "skin" in this case is the model's vertices.
> Similarly, the terms *bone* and *joint*, though different in the context of anatomy, are interchangeable terms in the context of skeletal animation.

An advantage of skeletal animation is that the same skeleton can work for several different characters. For example, it's common in a game for all humanoid characters to share the same skeleton. This way, the animator creates one set of animations for the skeleton, and all characters can then use those animations.

Furthermore, many popular 3D model authoring programs such as Autodesk Maya and Blender support skeletal animations. Thus, artists can use these tools to author the skeletons and animations for characters. Then, as with 3D models, you can write exporter plugins to export into the preferred format for the game code. As with 3D models this book uses a JSON-based file format for the skeleton and animations. (As a reminder, the book's code on GitHub includes an exporter for Epic Games's Unreal Engine, in the `Exporter` directory.)

The remainder of this section looks at the high-level concepts and mathematics that drive skeletal animation. The subsequent section then dives into the details of implementing skeletal animation in game code.

### Skeletons and Poses

The usual representation of a **skeleton** is as a hierarchy (or tree) of bones. The **root bone** is the base of the hierarchy and has no parent bone. Every other bone in the skeleton has a single parent bone. Figure 12.1 illustrates a simple skeletal hierarchy for a humanoid character. The spine bone is a child of the root bone, and then in turn the left and right hip bones are children of the spine bone.

![](img/e9afcec1487716b0ef80d7e7c09869c8_785_0.png)

Figure 12.1 Character with a basic skeleton with some bones labeled

This bone hierarchy attempts to emulate anatomy. For example, if a human rotates her shoulder, the rest of the arm follows that rotation. With a game skeleton, you might represent this by saying the shoulder bone is the parent of the elbow bone, the elbow bone is the parent of the wrist bone, and the wrist bone is the parent of the finger bones.

Given a skeleton, a **pose** represents a configuration of the skeleton. For example, if a character waves hello in an animation, there is one pose during the animation where the character's hand bone is raised up to wave. An animation is then just a sequence of poses the skeleton transitions between over time.

The **bind pose** is the default pose of the skeleton, prior to applying any animation. Another term for bind pose is **t-pose** because, typically, the character's body forms a T

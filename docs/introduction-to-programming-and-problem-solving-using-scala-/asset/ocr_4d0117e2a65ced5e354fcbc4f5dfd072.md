# Introduction to Programming and Problem-Solving Using Scala

You can see what this game looks like in figure 12.11. The first 28 lines have various declarations. They are followed by the declaration of the app with a Stage and Scene. Lines 35 to 46 build a simple layout with a MenuBar at the top of a BorderPane and a Canvas at the center.

Lines 48 to 61 set up the event handling on the canvas. Mouse presses and drags add elements to the puddles list. The key presses and releases change the value of some variables. The actual movement of the player occurs in the movePlayer function on lines 72 to 78. This has two advantages: it allows the motion to be part of the normal timing of the game, to easily work with multiple keys being held down at the same time. It also allows diagonal motion, which would not work if we moved the player in the onKeyPressed handler way we did in the Pong game.

Lines 64 to 103 have some helper functions that are just used to break up the logic and make the code easier to read and write.

Lines 105 to 140 have the AnimationTimer declaration, which is where the real work is done. This includes the helper functions for moving the player, enemies, and evaporating the puddles. It also has code to create new enemies at regular intervals. After that code is the code that actually draws the game to the GraphicsContext of the Canvas which was stored in the variable gt on line 62. This starts by filling a rectangle that is the size of the whole canvas with black, then it draws the puddles, enemies, and the player. If the player has died, a text message is also drawn.

# Thread Handling

One of aspects of ScalaFX that we have not really worried about is the fact that certain types of changes should only be made in certain parts of the code. In particular, ScalaFX has a thread that is used to handle all the events and drawing that goes on. A proper discussion of threads goes beyond the scope of this book (it is covered in "Object-Orientation, Abstraction, and Data-Structures using Scala\ but there are times when you need to worry about it. The issue is that you should only change values of things in the scene graph, or draw to a GraphicsContext inside of that thread. That means either inside of an event handler or in a timer, basically something that is called by ScalaFX. If you want to make changes to values or draw things outside of those chunks of code, you need to schedule it to run in the event thread. You can do this by calling Process.runLater(op) where op is a pass-by-name anyway. Whatever code you put into there will run in the ScalaFX event thread when it is free to do so. This is presented here because you might find it handy to use the GraphicsContext outside of the event or timer.

# 12.7 Effects

Another cool feature of ScalaFX is that it allows you to attach effects to Nodes. The different effects that you can add are all in the scalafx.scene.effect package, and they are subtypes of Effect. Here is a list of the different options, how to create them, and

bottom walls are positioned 140 units apart in the *y*-direction. We give both a width of 5 units. This width is an arbitrary value. You can change the width to make the game look as you want it to. If you change this, you’ll also have to change the collision detection code—you’ll see why when we discuss the collision logic. For the left and right walls to stretch between the top and bottom walls, they must be 145 units long (140 plus the half-width of each wall). So the *x*-scaling factor for the left and right walls is 1.45. The left and right walls are also given a width of 5 units and are positioned 185 units apart in the *x*-direction. For the top and bottom walls to stretch between the left and right walls, they must be 195 units long, so their *y*-scaling factor is 1.95.

## Add the Text

We use an Ogre Overlay to display the score of the game as text. An Overlay refers to anything you want to render on top of the 3D elements of the scene. We use Overlays only for text in this chapter. The Overlay is defined by a script saved in a `.overlay` file.

Overlays are composed of OverlayElements. The first element in an Overlay must be an OverlayContainer. An OverlayContainer can hold any type of OverlayElement. A TextAreaOverlayElement holds the text that will be displayed on the screen. Every object in an Overlay has three main attributes—metrics mode, position and size. The position is determined by the top-left corner of the object and is always relative to the parent OverlayContainer of the object. Size is determined by width and height. The metrics mode determines how the object is positioned and sized. Pixel mode will size the object based on the width and height declared in pixels. Relative mode will position and size the object relative to the size of the parent OverlayContainer (or the window if it’s the outermost OverlayContainer). In relative mode, size and position values range from 0.0 to 1.0—think of it as a percentage of the parent OverlayElement’s size. If you position an element at (0.0, 0.0), it will be at the top-left corner of the parent element; (0.5, 0.0) would be 50 percent across the top.

To display the score, we create an Overlay (Fig. 27.14). Line 2 names the Overlay Score. A single overlay file can hold several overlay definitions. Ogre will reference each Overlay by the name rather than the file. The *z*-order of the Overlay (line 5) is used to define what this Overlay should be rendered over. When using multiple Overlays, an Overlay with a higher *z*-order will be rendered on top of an Overlay with a lower *z*-order. Lines 8–58 create a PanelOverlayElement container that holds two TextAreaOverlayElements. The OverlayContainer is positioned in the top-left corner of the screen (lines 13–14) and runs along the entire width (line 17). The container is 10 percent of the height of the window (line 18). The first TextAreaOverlayElement (lines 21–38) is positioned at the top of the container, 5 percent away from the left side, runs half the width and is the same height as the container (lines 28–31). The other TextAreaOverlayElement (lines 40–57) is positioned 69 percent of the way across the top of the container and runs to the end. The TextAreaOverlayElements also declare a font to use (which is defined by a script in a `.fontdef` file in the PongResources folder), the character height, font color (note the British spelling, “colour”) and the section (lines 34–37 and 53–56).

```text
52    // set font used for caption and set the size and color
53    font_name BlueBold
54    char_height 0.05
55    colour 1.0 0 0
56    caption Player 2 Score: 0
57  }
58 }
59}
```

**Fig. 27.14** | Overlay script to display the score. (Part 2 of 2.)

Lines 115–117 of class Pong (Fig. 27.5) display the score on the screen. We use the static member function getString of class OverlayManager to get a pointer to the OverlayManager object. We use that object to get a pointer to the score Overlay, then we call the show function to display it on the screen. When a player scores, we need to update the text within the Overlay to reflect the change (lines 192–210). First we create the new text. Then we get a pointer to the appropriate TextAreaOverlayElement from the OverlayManager and use the TextAreaOverlayElement member function setCaption to replace the text.

Figure 27.15 is the `.fontdef` file that defines the BlueBold font. Line 2 gives the font a name that Ogre will refer to. Line 5 tells Ogre what type of font it is. TrueType is a common font file format (a `.ttf` file). The source (line 8) is the file that contains the font. We put the `.ttf` file in the same folder as the `.fontdef` file. If you place the two files in different locations, you’ll have to specify the path to the .ttf file in line 8 or add the folder containing the .ttf file as a resource location (discussed in Section 27.4.8).

```text
 1    // define the BlueBold font
 2    BlueBold
 3    {
 4      // define the font type
 5      type truetype
 6
 7      // set the source file for the font
 8      source bluebold.ttf
 9
10      // set the font size
11      size 16
12
13      // set the font resolution (96 is standard)
14      resolution 96
15    }
```

**Fig. 27.15** | BlueBold font definition script.

### 27.4.4 Animation and Timers

Now that we know how to draw a ball on the screen, animating it and making it move around the screen is straightforward. The function moveBall (Fig. 27.8, lines 54–108) moves the Ball around the screen. In most Pong games, the ball can travel at many different angles. However, since we are just starting out with Ogre, we want to keep things as simple as possible. For this reason, in our Pong game, the ball has only four possible directions of travel: down-right, up-right, down-left, and up-left—all at 45-degree angles to the x- and y-axes in our program.

Line 56 actually makes the Ball move; the rest of the function controls collisions with various objects within the scene, as we’ll see shortly. The translate function takes as an argument a Vector3, which is a three-dimensional vector as defined by Ogre. The vector represents the direction and distance to move the Ball. We pass the translate function the Ball’s direction multiplied by the distance to travel (speed × time) to determine the final vector. The speed parameter is the number of units the ball will move per second. The time parameter is the number of seconds since the last time the Ball was moved. We see where this comes from in just a moment. SceneNode translations are done in parent space by default. That means that the node is translated with respect to its parent node’s position and orientation (i.e., the direction the node is facing). Translations can also be performed in world or local space by adding another parameter to the translate function (TS_LOCAL or TS_WORLD). Translations in world space are done with respect to the origin of the scene (0, 0, 0). Translations in local space are done with respect to the node’s origin (wherever the node is positioned and whichever direction it’s facing).

To continuously move the Ball across the screen, call the moveBall function each time a new frame is rendered. Figure 27.4 defines the Pong class, our game’s main driving class, which inherits from the Ogre class FrameListener. A FrameListener is a class that processes Ogre::FrameEvents. A FrameEvent occurs every time a frame begins or ends. Every FrameListener has two functions, frameStarted and frameEnded (lines 29–30). These functions both return a bool. Ogre keeps rendering frames until one of these functions returns false. We use the frameStarted function (Fig. 27.5, lines 271–295) to control the animation of our Ball, specifically line 278. This function is called by Ogre before each new frame is rendered. Before every frame, the frameStarted function calls the Ball class member function moveBall, which continuously moves the Ball across the screen. As discussed earlier, controlling the speed of the animation is vital to creating smooth motion. Frame rates (i.e., how quickly the scene gets redrawn) may vary greatly on different machines, so the Ball could move at a different speed on each one. For that reason we pass the FrameEvent’s data member timeSinceLastFrame, in seconds, to the moveBall function. We multiply this time by the Ball’s speed to determine the distance the Ball should move across the screen. This is an example of using a timer to control animation.

### 27.4.5 User Input

Now we discuss moving the Paddle up and down on the screen with the movePaddle function of class Paddle (Fig. 27.11, lines 37–46). To move the Paddle, we again use the SceneNode function translate (line 39). Rather than moving the Paddle based on time, we move it based on user input from the keyboard. The user specifies a direction, up or down, by pressing the corresponding key, and the Paddle moves accordingly. The direction is then passed to movePaddle as a Vector3.

Ogre does not directly support user input from devices such as the keyboard, mouse or joystick. The Ogre SDK does come with the Object Oriented Input System (OIS) for handling user input. It isn’t required that you use OIS for input with Ogre, but it’s a good choice.

We need to create an InputManager, a Keyboard and a KeyListener to handle the user input and control the calls to movePaddle. The InputManager is used to create the

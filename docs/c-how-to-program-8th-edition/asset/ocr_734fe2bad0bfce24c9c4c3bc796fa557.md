```
```cpp
267    return !quit; // quit = false if the user hasn't quit yet
268 } // end function frameEnded

270 // process game logic, return true if the next frame should be rendered
271 bool Pong::frameStarted( const FrameEvent &frameEvent )
272 {
273     keyboardPtr->capture(); // get keyboard events
274     // the game is not paused and the Ball should move
275     if ( !wait && !pause )
276     {
277         // move the Ball
278         ballPtr->moveBall( frameEvent.timeSinceLastFrame );
279     } // end if
280     // don't move the Ball if wait is true
281     else if ( wait )
282     {
283         // increase time if it is less than 4 seconds
284         if ( time < 4 )
285             // add the seconds since the last frame
286             time += frameEvent.timeSinceLastFrame;
287         else
288         {
289             wait = false; // shouldn't wait to move the Ball any more
290             time = 0; // reset the control variable to 0
291         } // end else
292     } // end else

294     return !quit; // quit = false if the user hasn't quit yet
295 } // end function frameStarted
```
```

**Fig. 27.5** | Pong class member-function definitions. (Part 7 of 7.)

Before we can display any graphics, we need to initialize the Ogre engine settings and create certain Ogre objects. The **OGRE Engine Rendering Setup** dialog box (Fig. 27.6) enables the user to choose the rendering settings, including which rendering subsystem to use (Direct3D or OpenGL), resolution, color depth, full-screen mode, and other options that are beyond the scope of this chapter. Direct3D is exclusively for Windows. OpenGL is supported on all major platforms. The resolution is defined by two values, width and height, which determine the number of pixels used to draw the scene. The resolution options for both rendering subsystems can range from 640 × 400 to 1680 × 1050 or higher, depending on your hardware. A higher resolution will produce more detailed graphics. If you choose to turn off full-screen mode, the resolution will also determine the size of the window in which the game is displayed. We run the game at a resolution of 800 × 600. A color depth of n bits means that 2ⁿ possible colors can be displayed on the screen. A lower color depth will make the program require less memory, but the graphics may not be as good. Direct3D and OpenGL each support 16-bit and 32-bit color depths. In 32-bit colors, only 24 bits are used for the color; the other eight bits represent the alpha value (i.e., transparency).

To display the dialog box, you must create a **Root** object (Fig. 27.5, line 28)—the Ogre object used to start the engine. The only Ogre object that can be created before Root is the LogManager—but that is beyond the scope of this book. Next, we call the
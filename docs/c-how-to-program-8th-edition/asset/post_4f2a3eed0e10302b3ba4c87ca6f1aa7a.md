
```cpp
// create the scene to be displayed
void Page::createScene()
{
    // get a pointer to the Score Overlay
    Overlay *scoreOverlayPtr =
        OverlayManager::getSingleton().getByName( "Score" );
    scoreOverlayPtr->show(); // show the Overlay

    // make the game objects
    ballPtr = new Ball( sceneManagerPtr ); // make the Ball
    ballPtr->addToScene(); // add the ball to the scene
    rightPaddlePtr = new Paddle( sceneManagerPtr, "RightPaddle", 90 );
    rightPaddlePtr->addToScene(); // add a Paddle to the scene
    leftPaddlePtr = new Paddle( sceneManagerPtr, "LeftPaddle", -90 );
    leftPaddlePtr->addToScene(); // add a Paddle to the scene

    // create the walls
    Entity entityPtr = sceneManagerPtr->
        createEntity( "WallLeft", "cube.mesh" ); // create the left wall
    entityPtr->setMaterialName( "wall" ); // set material for the left wall
    entityPtr->setNormaliseNormals( true ); // fix the normals when scaled

    // create the SceneNode for the left wall
    SceneNode *nodePtr = sceneManagerPtr->getRootSceneNode()->
        createChildSceneNode( "WallLeft" );
    nodePtr->attachObject( entityPtr ); // attach left wall to SceneNode
    nodePtr->setPosition( -95, 0, 0 ); // set the left wall's position
    nodePtr->setScale( .05, 1.45, .1 ); // set the left wall's size
    entityPtr = sceneManagerPtr->createEntity( "WallRight", "cube.mesh" );
    entityPtr->setMaterialName( "wall" ); // set material for right wall
    entityPtr->setNormaliseNormals( true ); // fix the normals when scaled

    // create the SceneNode for the right wall
    nodePtr = sceneManagerPtr->getRootSceneNode()->
        createChildSceneNode( "WallRight" );
    nodePtr->attachObject( entityPtr ); // attach right wall to SceneNode
    nodePtr->setPosition( 95, 0, 0 ); // set the right wall's position
    nodePtr->setScale( .05, 1.45, .1 ); // set the right wall's size
    entityPtr = sceneManagerPtr->createEntity( "WallBottom", "cube.mesh" );
    entityPtr->setMaterialName( "wall" ); // set material for bottom wall
    entityPtr->setNormaliseNormals( true ); // fix the normals when scaled

    // create the SceneNode for the bottom wall
    nodePtr = sceneManagerPtr->getRootSceneNode()->
        createChildSceneNode( "WallBottom" );
    nodePtr->attachObject( entityPtr ); // attach bottom wall to SceneNode
    nodePtr->setPosition( 0, -70, 0 ); // set the bottom wall's position
    nodePtr->setScale( 1.95, .05, .1 ); // set the bottom wall's size
    entityPtr = sceneManagerPtr->createEntity( "WallTop", "cube.mesh" );
    entityPtr->setMaterialName( "wall" ); // set the material for top wall
    entityPtr->setNormaliseNormals( true ); // fix the normals when scaled
}
```

*Fig. 27.5*  |  Pong class member-function definitions. (Part 4 of 7.)

```cpp
// if the game is not paused
if ( !pause )
{
   // process KeyEvents that apply when the game is not paused
   switch ( keyEventRef.key )
   {
   case OIS::KC_ESCAPE: // escape key hit: quit
      quit = true;
      break;
   case OIS::KC_UP: // up-arrow key hit: move the right Paddle up
      rightPaddlePtr->movePaddle( PADDLE_UP );
      break;
   case OIS::KC_DOWN: // down-arrow key hit: move the right Paddle down
      rightPaddlePtr->movePaddle( PADDLE_DOWN );
      break;
   case OIS::KC_A: // A key hit: move the left Paddle up
      leftPaddlePtr->movePaddle( PADDLE_UP );
      break;
   case OIS::KC_Z: // Z key hit: move the left Paddle down
      leftPaddlePtr->movePaddle( PADDLE_DOWN );
      break;
   case OIS::KC_P: // p key hit: pause the game
      pause = true; // set pause to true when the user pauses the game
      Overlay *pauseOverlayPtr =
         OverlayManager::getSingleton().getByName( "pauseOverlay" );
      pauseOverlayPtr->show(); // show the pause Overlay
      break;
   } // end switch
} // end if
else // game is paused
{
   // user hit 'R' on the keyboard
   if ( keyEventRef.key == OIS::KC_R )
   {
      pause = false; // set pause to false when user resumes the game
      Overlay *pauseOverlayPtr =
         OverlayManager::getSingleton().getByName( "pauseOverlay" );
      pauseOverlayPtr->hide(); // hide the pause Overlay
   } // end if
} // end else
return true;
} // end function keyPressed

// process key released events
bool Pong::keyReleased( const OIS::KeyEvent &keyEventRef )
{
   return true;
} // end function keyReleased

// return true if the program should render the next frame
bool Pong::frameEnded( const FrameEvent &frameEvent )
{
```

Fig. 27.5 | Pong class member-function definitions. (Part 6 of 7.)

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

**Fig. 27.5** | Pong class member-function definitions. (Part 7 of 7.)

Before we can display any graphics, we need to initialize the Ogre engine settings and create certain Ogre objects. The **OGRE Engine Rendering Setup** dialog box (Fig. 27.6) enables the user to choose the rendering settings, including which rendering subsystem to use (Direct3D or OpenGL), resolution, color depth, full-screen mode, and other options that are beyond the scope of this chapter. Direct3D is exclusively for Windows. OpenGL is supported on all major platforms. The resolution is defined by two values, width and height, which determine the number of pixels used to draw the scene. The resolution options for both rendering subsystems can range from 640 × 400 to 1680 × 1050 or higher, depending on your hardware. A higher resolution will produce more detailed graphics. If you choose to turn off full-screen mode, the resolution will also determine the size of the window in which the game is displayed. We run the game at a resolution of 800 × 600. A color depth of n bits means that 2ⁿ possible colors can be displayed on the screen. A lower color depth will make the program require less memory, but the graphics may not be as good. Direct3D and OpenGL each support 16-bit and 32-bit color depths. In 32-bit colors, only 24 bits are used for the color; the other eight bits represent the alpha value (i.e., transparency).

![](img/bfd978e7e9b192bab46ec2a89e481263_1269_0.png)

**Fig. 27.6** | OGRE Engine Rendering Setup dialog box.

To display the dialog box, you must create a **Root** object (Fig. 27.5, line 28)—the Ogre object used to start the engine. The only Ogre object that can be created before Root is the LogManager—but that is beyond the scope of this book. Next, we call the showConfigDialog function of the Root class (line 31) to display the dialog. Once you hit OK, Ogre saves the settings and uses them as the default settings the next time the dialog box is displayed. The program should end if the user selects Cancel, because the settings may not be properly configured and could cause errors. We throw a runtime_error if showConfigDialog returns false (i.e., the user selected Cancel).

Once the rendering subsystem and window options have been set, we can create the **RenderWindow**, a window in which Ogre will render graphics, by calling the **initialise** function of class Root (line 35). The first parameter, true, tells Ogre to create the window with the settings the user chose in the dialog box. Passing false to this parameter allows you to manually create the window at a later time. The second, "Pong", is the name of the window within the engine and will also appear in the title bar of the window if it isn’t full screen. Notice the British spelling of **initialise** and of **colour** in Fig. 27.6, reflecting Ogre’s origin in the United Kingdom.

### 27.4.2 Creating a Scene

Now that we’ve initialized Ogre and set up a window to render our graphics, we’ll add some objects to create our scene—the collection of images that we display on the screen.

#### SceneManager

To control the scene we use Ogre’s **SceneManager** object (line 38). The SceneManager manages the scene graph, a data structure that contains all the objects in the scene, both visible and invisible. The SceneManager is used to create objects that will be added to the scene graph and determines which objects will be rendered. Excluding objects that are not within the visible scene from being rendered, known as culling, decreases rendering

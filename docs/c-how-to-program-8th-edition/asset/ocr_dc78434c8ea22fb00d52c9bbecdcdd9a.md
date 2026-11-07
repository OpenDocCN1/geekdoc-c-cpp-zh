```
Light *lightPtr = sceneManagerPtr->createLight( "Light" ); // a Light
lightPtr->setPosition( 0, 0, 50 ); // set the light's position

unsigned long hWnd; // variable to hold the window handle
windowPtr->getCustomAttribute( "WINDOW", &hWnd ); // get window handle
OIS::ParamList paramList; // create an OIS ParamList

// add the window to the ParamList
paramList.insert( OIS::ParamList::value_type( "WINDOW",
    Ogre::StringConverter::toString( hWnd ) ) );

// create the InputManager
inputManagerPtr = OIS::InputManager::createInputSystem( paramList );
keyboardPtr = static_cast< OIS::Keyboard * >( inputManagerPtr->
    createInputObject( OIS::OISKeyboard, true ) ); // create a Keyboard
keyboardPtr->setEventCallback( this ); // add a KeyListener

rootPtr->addFrameListener( this ); // add this Pong class as a FrameListener

// load resources for Pong
ResourceGroupManager::getSingleton().addResourceLocation(
    "resources", "FileSystem", "Pong" );
ResourceGroupManager::getSingleton().initialiseAllResourceGroups();

quit = pause = false; // player has not quit or paused the game
time = 0; // initialize the time since Ball was reset to 0
} // end Pong constructor

// Pong destructor erases objects contained in a Pong object
Pong::~Pong()
{
    // free dynamically allocated memory for Keyboard
    inputManagerPtr->destroyInputObject( keyboardPtr );
    OIS::InputManager::destroyInputSystem( inputManagerPtr );

    // free dynamically allocated memory for Root
    delete rootPtr; // release memory pointer points to
    rootPtr = 0; // point pointer at 0

    // free dynamically allocated memory for Ball
    delete ballPtr; // release memory pointer points to
    ballPtr = 0; // point pointer at 0

    // free dynamically allocated memory for Paddle
    delete leftPaddlePtr; // release memory pointer points to
    leftPaddlePtr = 0; // point pointer at 0

    // free dynamically allocated memory for Paddle
    delete rightPaddlePtr; // release memory pointer points to
    rightPaddlePtr = 0; // point pointer at 0
} // end Pong destructor
```

Fig. 27.5 | Pong class member-function definitions. (Part 3 of 7.)
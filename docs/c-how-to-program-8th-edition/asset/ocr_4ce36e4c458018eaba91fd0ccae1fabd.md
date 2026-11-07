```
#include <OgreStringConverter.h> // OgreStringConverter class definition
#include <OIS/OISEvents.h> // OISEvents.h class definition
#include <OIS/OISInputManager.h> // OISInputManager class definition
#include <OIS/OISKeyboard.h> // OISKeyboard class definition
#include "Ball.h" // Ball class definition
#include "Paddle.h" // Paddle class definition
#include "Pong.h" // Pong class definition
using namespace std;
using namespace Ogre;

int Pong::player1Score = 0; // initialize player 1's score to 0
int Pong::player2Score = 0; // initialize player 2's score to 0
bool Pong::wait = false; // initialize wait to false

// directions to move the Paddles
const Vector3 PADDLE_DOWN = Vector3(0, -15, 0);
const Vector3 PADDLE_UP = Vector3(0, 15, 0);

// constructor
Pong::Pong()
{
    rootPtr = new Root(); // initialize Root object

    // use the Ogre Config Dialog Box to choose the settings
    if ( !rootPtr->showConfigDialog() ) // user canceled the dialog box
        throw runtime_error( "User Canceled Ogre Setup Dialog Box." );

    // get a pointer to the RenderWindow
    windowPtr = rootPtr->initialise( true, "Pong" );

    // create the SceneManager
    sceneManagerPtr = rootPtr->createSceneManager( ST_GENERIC );

    // create the Camera
    cameraPtr = sceneManagerPtr->createCamera( "PongCamera" );
    cameraPtr->setPosition( Vector3(0, 0, 200 ) ); // set Camera position
    cameraPtr->lookAt( Vector3( 0, 0, 0 ) ); // set where the Camera looks
    cameraPtr->setNearClipDistance( 5 ); // near distance Camera can see
    cameraPtr->setFarClipDistance( 1000 ); // far distance Camera can see

    // create the Viewport
    viewportPtr = windowPtr->addViewport( cameraPtr );
    viewportPtr->setBackgroundColour( ColourValue( 0, 0, 0 ) );

    // set the Camera's aspect ratio
    cameraPtr->setAspectRatio( Real( viewportPtr->getActualWidth() /
        ( viewportPtr->getActualHeight() ) ) );

    // set the scene's ambient light
    sceneManagerPtr->setAmbientLight( ColourValue( 0.75, 0.75, 0.75 ) );

    // create the Light
```

Fig. 27.5 | Pong class member-function definitions. (Part 2 of 7.)
```
```cpp
// Ball.cpp
// Ball class member-function definitions
#include <Ogre.h> // Ogre class definitions
#include <OgreAL.h> // OgreAL class definitions
#include "Ball.h" // Ball class definition
#include "Paddle.h" // Paddle class definition
#include "Pong.h" // Pong class definition
using namespace Ogre;

// Ball constructor
Ball::Ball( SceneManager *ptr )
{
    sceneManagerPtr = ptr; // set pointer to the SceneManager
    soundManagerPtr = new OgreAL::SoundManager(); // create SoundManager
    speed = 100; // speed of the Ball
    direction = Vector3( -1, 1, 0 ); // direction of the Ball
} // end Ball constructor

// Ball destructor
Ball::~Ball()
{
    // empty body
} // end Ball destructor

// add the Ball to the scene
void Ball::addToScene()
{
    // create Entity and attach it to a node in the scene
    Entity *entityPtr =
        sceneManagerPtr->createEntity( "Ball", "sphere.mesh" );
    entityPtr->setMaterialName( "ball" ); // set material for the Ball
    entityPtr->setNormaliseNormals(true); // fix the normals when scaled
    nodePtr = sceneManagerPtr->getRootSceneNode()->
        createChildSceneNode( "ball" ); // create a SceneNode
    nodePtr->attachObject( entityPtr ); // attach the Entity to the SceneNode
    nodePtr->setScale( .05, .05, .05 ); // scale SceneNode

    // attach sounds to Ball so they will play from where Ball is
    wallSoundPtr = soundManagerPtr->
        createSound( "wallSound", "wallSound.wav", false );
    nodePtr->attachObject( wallSoundPtr ); // attach a sound to SceneNode
    paddleSoundPtr = soundManagerPtr->
        createSound( "paddleSound", "paddleSound.wav", false );
    nodePtr->attachObject( paddleSoundPtr ); // attach sound to SceneNode
    scoreSoundPtr = soundManagerPtr->
        createSound( "cheer", "cheer.wav", false ); // create a Sound

    // attach the score sound to this pong node generated at 0,0
    sceneManagerPtr->getRootSceneNode()->createChildSceneNode( "score" )->
        attachObject( scoreSoundPtr );
} // end function addToScene
```
```

Fig. 27.8 | Ball class member-function definitions. (Part 1 of 4.)
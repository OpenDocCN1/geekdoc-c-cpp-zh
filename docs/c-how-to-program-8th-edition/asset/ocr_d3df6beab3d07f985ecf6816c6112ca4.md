![](bbox=[0.224, 0.116, 0.776, 0.444])

**Fig. 27.3** | Pong game objects.

handling user input from the keyboard. Lines 29–30 define the function prototypes for performing game logic between frames. We also declare pointers to important Ogre objects (lines 38–42), input handling objects (lines 45–46) and the game objects (lines 49–51). Lines 54–56 define some variables used to control the behavior of the game—we’ll discuss these later.

```
```cpp
// Pong.h
// Pong class definition (represents a game of Pong).
#ifndef PONG_H
#define PONG_H

#include <Ogre.h> // Ogre class definitions
#include <OIS/OISObjects.h> // OISEvents class definition
#include <OIS/OISInputManager.h> // OISInputManager class definition
#include <OIS/OISKeyboard.h> // OISKeyboard class definition
using namespace Ogre;

class Ball; // forward declaration of class Ball
class Paddle; // forward declaration of class Paddle

enum Players { PLAYER1, PLAYER2 };

class Pong : public FrameListener, public OIS::KeyListener
{
public:
    Pong(); // constructor
```
```

**Fig. 27.4** | Pong class definition (represents a game of Pong). (Part 1 of 2.)
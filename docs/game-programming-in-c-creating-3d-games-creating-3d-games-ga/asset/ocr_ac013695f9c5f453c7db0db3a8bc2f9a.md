```
State mState;

// Transform

Vector2 mPosition; // Center position of actor

float mScale; // Uniforms scale of actor (1.0

float mRotation; // Rotation angle (in radians)

// Components held by this actor

std::vector<class Component*> mComponents;

class Game* mGame;
};
```

The Actor class has several notable features. The state enum tracks the status of the actor. For example, Update only updates the actor when in the EActive state. The EDead state notifies the game to remove the actor. The Update function calls UpdateComponents first and then UpdateActor. UpdateComponents loops over all the components and updates each in turn. The base implementation of UpdateActor is empty, but Actor subclasses can write custom behavior in an overridden UpdateActor function.

In addition, the Actor class needs access to the Game class for several reasons, including to create additional actors. One approach is to make the game object a singleton, a design pattern in which there is a single, globally accessible instance of a class. But the singleton
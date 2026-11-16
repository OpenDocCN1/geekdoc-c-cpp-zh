```
// Getters/setters for private variables

// ...

private:
// The maximum forward/angular speeds
float mMaxForwardSpeed;
float mMaxAngularSpeed;

// Keys for forward/back movement
int mForwardKey;
int mBackKey;

// Keys for angular movement
int mClockwiseKey;
int mCounterClockwiseKey;
};
```

Listing 3.5 shows the implementation of InputComponent :: ProcessInput. You first set the forward speed to zero and then determine the correct forward speed based on the keys pressed. You then pass this speed into the inherited SetForwardSpeed function. Note that if the user presses both forward and back keys or neither of the keys, the forward speed becomes zero. You use similar code for setting the
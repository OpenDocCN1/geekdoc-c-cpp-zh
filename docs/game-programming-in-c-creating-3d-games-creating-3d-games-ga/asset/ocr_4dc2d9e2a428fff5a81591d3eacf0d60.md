```
const InputState& GetState() const { return mState

private:

InputState mState;

};
```

To integrate this code into the game, you add an InputSystem pointer to the member data of Game called mInputSystem. Game :: Initialize allocates and initializes InputSystem and Game :: Shutdown shuts down and deletes it.

Next, you change the declaration of ProcessInput in both Actor and Component to the following:

Click here to view code image

```
void ProcessInput(const InputState& state);
```

Recall that in Actor, ProcessInput is not overridable because it calls ProcessInput on all the attached components. However, actors also have an overridable ActorInput function for any input specific to that actor. So, you similarly change the declaration of ActorInput to take in a constant InputState reference.

Finally, the implementation of Game :: ProcessInput changes to the following outline of steps:
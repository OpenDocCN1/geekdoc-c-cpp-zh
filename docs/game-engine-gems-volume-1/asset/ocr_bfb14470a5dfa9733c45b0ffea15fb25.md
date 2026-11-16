__NotifySubscribers() to send all the observers the update.

# Listing 26.5: The set implementation for the currentState member of the GameState class.

```
public State currentState
{
    get { return this._currentState; }

    set
    {
        if (this._currentState != value)
        {
            this._currentState = value;
            this._NotifySubscribers();
        }
    }
}
```

That's about all there is for the game state manager's role in its own observation. The ball is now in the observer's court. Having received an update, it must be able to take action based on the data it has received.

[2]This is a C# implementation, and a C++ implementation is similar. Other languages provide keywords such as implements or extends to indicate relationships among various structures. Be sure to use the appropriate syntax for the programming language your game uses.
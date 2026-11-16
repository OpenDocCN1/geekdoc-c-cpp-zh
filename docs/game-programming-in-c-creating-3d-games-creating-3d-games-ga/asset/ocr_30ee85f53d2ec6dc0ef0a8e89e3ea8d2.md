```
ButtonState KeyboardState::GetKeyState(SDL_Scancode {
    if (mPrevState[keyCode] == 0)
    {
        if (mCurrState[keyCode] == 0)
        { return ENone; }
        else
        { return EPressed; }
    }
    else // Prev state must be 1
    {
        if (mCurrState[keyCode] == 0)
        { return EReleased; }
        else
        { return EHeld; }
    }
}
```

With this `KeyboardState` code, you can still access the value of a key with the `GetKeyValue` function. For example, the following checks if the current value of the
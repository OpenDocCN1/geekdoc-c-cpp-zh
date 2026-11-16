```
SDL_CONTROLLER_BUTTON_MAX);
```

Finally, in Update, loop over the mCurrButtons array and set the value of each element to the result of the SDL_GameControllerGetButton call that queries the state of that button:

Click here to view code image

```
for (int i = 0; i < SDL_CONTROLLER_BUTTON_MAX; i++)
{
    mState.Controller.mCurrButtons[i] =
        SDL_GameControllerGetButton(mController,
        SDL_GameControllerButton(i));
}
```

With this code, you can then query the state of a specific game controller button, using a pattern like the keyboard and mouse buttons. For example, this code checks if the A button on the controller has a positive edge this frame:

Click here to view code image

```
if (state.Controller.GetButtonState(SDL_CONTROLLER_BU
```

# Analog Sticks and Triggers
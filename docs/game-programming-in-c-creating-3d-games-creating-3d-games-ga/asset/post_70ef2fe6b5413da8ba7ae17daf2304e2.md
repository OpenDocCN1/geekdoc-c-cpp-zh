
{
    switch (event.type)
    {
    case SDL_MOUSEWHEEL:
        mState.Mouse.mScrollWheel = Vector2 (
            static_cast<float>(event.wheel.x),
            static_cast<float>(event.wheel.y));
        break;
    default:
        break;
    }
}

Next, because the mouse wheel event only triggers on frames where the scroll wheel moves, you need to make sure to reset the mScrollWheel variable during PrepareForUpdate:

Click here to view code image

```
mState.Mouse.mScrollWheel = Vector2::Zero;
```

This ensures that if the scroll wheel moves on frame 1 but doesn't move on frame 2, you don't erroneously report the same scroll value on frame 2.

With this code, you can now access the scroll wheel state every frame with the following:

Click here to view code image

```
Vector2 scroll = state.Mouse.GetScrollWheel();
```

## CONTROLLER INPUT

For numerous reasons, detecting controller input in SDL is more complex than for the keyboard and mouse. First, a controller has a much greater variety of sensors than a keyboard or mouse. For example, a standard Microsoft Xbox controller has two analog joysticks, a directional pad, four standard face buttons, three special face buttons, two bumper buttons, and two triggers—which is a lot of different sensors to get data from.

Furthermore, while PC/Mac users have only a single keyboard or mouse, it’s possible to have multiple controllers connected. Finally, controllers support **hot swapping**, which means it’s possible to plug and unplug controllers while a program is running. Combined, these elements add complexity to handling controller input.

> **note**
> Depending on the controller and your platform, you may need to first install a driver for your controller in order for SDL to detect it.

Before you can use a controller, you must first initialize the SDL subsystem that handles controllers. To enable it, simply add the SDL_INIT_GAMECONTROLLER flag to the SDL_Init call in Game::Initialize:

Click here to view code image

```
SDL_Init(SDL_INIT_VIDEO | SDL_INIT_AUDIO | SDL_INIT_GAMECONTROLLER);
```

## Enabling a Single Controller

For now, assume that you're using only a single controller and that this controller is plugged in when the game starts. To initialize the controller, you need to use the SDL_GameControllerOpen function. This function returns a pointer to an SDL_Controller struct upon successful initialization or nullptr if it fails. You can then use the SDL_Controller* variable to query the state of the controller.

For this single controller, you first add an SDL_Controller* pointer called mController to the InputState member data. Then, add the following call to open controller 0:

Click here to view code image

```
mController = SDL_GameControllerOpen(0);
```

To disable a controller, you can call SDL_GameControllerClose, which takes the SDL_GameController pointer as its parameter.

> tip By default, SDL supports a handful of common controllers, such as the Microsoft Xbox controller. You can find controller mappings that specify the button layouts of many other controllers. The `SDL_GameControllerAddMappingsFromFile` function can load controller mappings from a supplied file. A community-maintained mapping file is available on GitHub at https://github.com/gabomdq/SDL_GameControllerDB.

Because you do not want to assume that the player has a controller, you must be vigilant to null check mController wherever you might want to access it in code.

## Buttons

Game controllers in SDL support many different buttons. SDL uses a naming convention that mirrors the button names of a Microsoft Xbox controller. For example, the names of the face buttons are A, B, X, and Y. Table 8.3 lists the different button constants defined by SDL, where * is a wildcard that denotes multiple possible values.

Table 8.3 SDL Controller Button Constants

| Button | Constant |
| --- | --- |
| A, B, X, or Y | SDL_CONTROLLER_BUTTON_* (replace * with A, B, X, or Y) |
| Back | SDL_CONTROLLER_BACK |
| Start | SDL_CONTROLLER_START |
| Pressing left/right stick | SDL_CONTROLLER_BUTTON_*_STICK (replace * with LEFT or RIGHT) |
| Left/right shoulder | SDL_CONTROLLER_BUTTON_*_SHOULDER (replace * with LEFT or RIGHT) |
| Directional pad | SDL_CONTROLLER_BUTTON_DPAD_* (replace * with UP, DOWN, LEFT, or RIGHT) |

Note that the left and right stick buttons are for when the user physically presses in the left/right stick. Some games use pressing in the right stick for sprinting, for example.

SDL does not have a mechanism to query the state of all controller buttons simultaneously. Instead, you must individually query each button via the SDL_GameControllerGetButton function.

However, you can take advantage of the fact that the enum for the controller button names defines an SDL_CONTROLLER_BUTTON_MAX member that is the number of buttons the controller has. Thus, the first pass of the ControllerState class, shown in Listing 8.6, contains arrays for both the current and previous button states. The code also has a Boolean so the game code can determine whether there's a controller connected. Finally, the class has declarations for the now-standard button value/state functions.

## Listing 8.6 Initial ControllerState Declaration

Click here to view code image

```
class ControllerState
{
public:
    friend class InputSystem;

    // For buttons
    bool GetButtonValue(SDL_GameControllerButton button
    ButtonState GetButtonState(SDL_GameControllerButton
        const;

    bool GetIsConnected() const { return mIsConnected;

private:
    // Current/previous buttons
    Uint8 mCurrButtons[SDL_CONTROLLER_BUTTON_MAX];
    Uint8 mPrevButtons[SDL_CONTROLLER_BUTTON_MAX];

    // Is this controlled connected?
    bool mIsConnected;
});
```

Then add an instance of `ControllerState` to `InputState`:

```
ControllerState Controller;
```

Next, back in `InputSystem::Initialize`, after you try to open controller 0, set the `mIsConnected` variable based on whether the `mController` pointer is non-null. You also clear out the memory for both `mCurrButtons` and `mPrevButtons`:

Click here to view code image

```
mState.Controller.mIsConnected = (mController != nullptr);
memset(mState.Controller.mCurrButtons, 0,
    SDL_CONTROLLER_BUTTON_MAX);
memset(mState.Controller.mPrevButtons, 0,
    SDL_CONTROLLER_BUTTON_MAX);
```

As with the keyboard, the code in `PrepareForUpdate` then copies the button states from current to previous:

Click here to view code image

```
memcpy(mState.Controller.mPrevButtons,
    mState.Controller.mCurrButtons,
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
if (state.Controller.GetButtonState(SDL_CONTROLLER_BUTTON_A)
```

## Analog Sticks and Triggers

SDL supports a total of six axes. Each analog stick has two axes: one in the x direction and one in the y direction. Furthermore, each of the triggers has a single axis. Table 8.4 shows the list of axes. (Once again, * denotes a wildcard.)

Table 8.4 SDL Controller Axis Constants

| Button | Constant |
| :--- | :--- |
| Left analog stick | SDL_CONTROLLER_AXIS_LEFT* (replace * with X or Y) |
| Right analog stick | SDL_CONTROLLER_AXIS_RIGHT* (replace * with X or Y) |
| Left/right triggers | SDL_CONTROLLER_AXIS_TRIGGER* (replace * with LEFT or RIGHT) |

For triggers, the value ranges from 0 to 32,767, with 0 meaning there is no pressure on the trigger. For the analog stick axes, the value ranges from -32,768 to 32,767, with 0 representing centered. A positive y-axis value corresponds to down on the analog stick, and a positive x-axis value corresponds to right.

However, an issue with continuous input such as these axes is that the ranges specified by the API are theoretical. Each individual device has its own imprecisions. You can observe this behavior by releasing one of the analog sticks, which returns the stick to its center. You might reasonably expect that because the

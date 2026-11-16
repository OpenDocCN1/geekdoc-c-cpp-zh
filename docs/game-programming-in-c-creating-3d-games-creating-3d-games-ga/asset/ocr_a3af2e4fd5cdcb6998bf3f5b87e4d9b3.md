```
mState.Mouse.mCurrButtons = SDL_GetMouseState(&x,
}
mState.Mouse.mMousePos.x = static_cast<float>(x);
mState.Mouse.mMousePos.y = static_cast<float>(y);
```

With this code, you can now enable relative mouse mode and access the relative mouse position via MouseState.

# Scroll Wheel

For the scroll wheel, SDL does not provide a function to poll the current state of the wheel. Instead, SDL generates the SDL_MOUSEWHEEL event. To support this in the input system, then, you must first add support for passing SDL events to InputSystem. You can do this via a ProcessEvent function, and then you update the event polling loop in Game::ProcessInput to pass the mouse wheel event to the input system:

Click here to view code image

```
SDL_Event event;
while (SDL_PollEvent(&event))
{
switch (event.type)
{
```
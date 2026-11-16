```
// Clamp f between 0.0f and 1.0f
f = Math::Clamp(f, 0.0f, 1.0f);
// Normalize the vector, and then scale it to t
// fractional value
dir *= f / length;
}
return dir;
}
```

Next, add two Vector2s to ControllerState for the left and right sticks, respectively. You can then add code in InputSystem::Update to grab the values of the two axes for each stick and then run Filter2D to get the final analog stick value. For example, the following code filters the left stick and saves the result in the controller state:

# Click here to view code image

```
x = SDL_GameControllerGetAxis(mController,
SDL_CONTROLLER_AXIS_LEFTX);
y = -SDL_GameControllerGetAxis(mController,
SDL_CONTROLLER_AXIS_LEFTY);
```
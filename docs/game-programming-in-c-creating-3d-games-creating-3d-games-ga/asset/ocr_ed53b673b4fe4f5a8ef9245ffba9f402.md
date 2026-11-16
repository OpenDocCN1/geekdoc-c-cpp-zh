```
// Update position based on strafe
pos += mOwner->GetRight() * mStrafeSpeed * deltaTime
mOwner->SetPosition(pos);
}
```

Then in `FPSActor::ActorInput`, you can detect the A/D keys and adjust the strafe speed as needed. Now the character can move with standard first-person WASD controls.

The left/right rotation also already exists in `MoveComponent` via the angular speed. So, the next task is to convert mouse left/right movements to angular speed. First, the game needs to enable relative mouse mode via `SDL_RelativeMouseMode`. Recall from Chapter 8, “Input Systems,” that relative mouse mode reports the change in (x, y) values per frame, as opposed to absolute (x, y) coordinates. (Note that in this chapter, you will directly use SDL input functions rather than the input system created in Chapter 8.)

Converting the relative x movement into an angular speed only requires a few calculations, shown in Listing 9.1. First, `SDL_GetRelativeMouseState` retrieves the (x, y) motion. The `maxMouseSpeed` constant is an expected maximum amount of relative motion possible per frame, though this might be an in-game setting. Similarly, `maxAngularSpeed` converts the motion into a rotation per second. You then take the reported x value,
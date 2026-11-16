```
// (In InputSystem::PrepareForUpdate...)
memcpy(mState.Keyboard.mPrevState,
mState.Keyboard.mCurrState,
SDL_NUM_SCANCODES);
```
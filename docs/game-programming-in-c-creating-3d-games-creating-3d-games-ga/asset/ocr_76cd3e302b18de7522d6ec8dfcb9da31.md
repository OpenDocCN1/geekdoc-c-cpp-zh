```
};
```

The implementations for most of the `SoundEvent` member functions have very similar syntax. They call `GetEventInstance` to get an `EventInstance` pointer and then call some function on the `EventInstance`. For example, the implementation of `SoundEvent::SetPaused` is as follows:

# Click here to view code image

```
void SoundEvent::SetPaused(bool pause)
{
    auto event = mSystem ?
    mSystem->GetEventInstance(mID) : nullptr;

    if (event)
    {
        event->setPaused(pause);
    }
}
```

Note how the code validates that both the `mSystem` and event pointer are non-null. This ensures that even if the ID is not in the map, the function will not crash. Similarly, the `SoundEvent::IsValid` function returns
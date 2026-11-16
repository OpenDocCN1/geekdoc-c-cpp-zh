transform matrix and converts it into FMOD's 3D attributes. This makes it simple to pass in the world transform matrix of an Actor to update the position and orientation of the event. Note that this function does not need to invert the matrix because the matrix is already in world space. However, it's still necessary to convert between the game and FMOD coordinate systems.

# Listing 7.7 SoundEvent's Is3D and Set3DAttributes Implementation

Click here to view code image

```
bool SoundEvent::Is3D() const
{
    bool retVal = false;
    auto event = mSystem ? mSystem->GetEventInstance(n
    if (event)
    {
        // Get the event description
        FMOD::Studio::EventDescription* ed = nullptr;
        event->getDescription(&ed);
        if (ed)
        {
            ed->is3D(&retVal); // Is this 3D?
```
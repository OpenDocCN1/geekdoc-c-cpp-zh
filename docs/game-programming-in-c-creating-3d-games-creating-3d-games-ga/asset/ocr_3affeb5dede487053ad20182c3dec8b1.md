AudioSystem. But because SoundEvent needs access to this function, SoundEvent is declared as a friend of AudioSystem.

Listing 7.5 gives the declaration of SoundEvent. Most notably, its member data includes a pointer to the AudioSystem and the ID. Note that while the default constructor is public, the constructor with parameters is protected. Because AudioSystem is a friend of SoundEvent, only AudioSystem has access to this constructor. This ensures that only AudioSystem can assign IDs to SoundEvents. The rest of the functions in SoundEvent are wrappers for various event instance functionality, such as pausing sound events, changing their volume, and setting event parameters.

# Listing 7.5 SoundEvent Declaration

Click here to view code image

```
class SoundEvent
{
public:
    SoundEvent();
    // Returns true if associated FMOD event instance
    bool IsValid();
    // Restart event from beginning
    void Restart();
```
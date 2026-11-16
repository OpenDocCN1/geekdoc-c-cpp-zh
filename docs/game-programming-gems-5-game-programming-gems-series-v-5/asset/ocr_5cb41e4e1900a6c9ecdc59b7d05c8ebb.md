To be able to dynamically control the properties of a group, the system will need to update each affected sound’s properties when the group’s properties are changed. That is, when a call like `SndSetGroupVolume()` is made, the system will need to access and update each currently active sound that is part of the group.

In APIs that manage playing sounds as objects (not necessarily C++ objects but architectural objects), like OpenAL and DirectSound, this commonly involves keeping a list of all active sounds. When group commands are issued, the list is walked and all appropriate sounds are updated.

In “track”-based APIs, like FMod and the Miles Sound System, it is likely that your wrapper API already tracks which sounds are playing on which channels, so group management may be a bit easier to implement.

# Simplified, One-Shot Sounds

One-shot sounds are short effects that a game plays and never needs to control. Gunshots and footsteps are good examples. In many cases, wrapper APIs include simplified calls to play back one-shot sounds without exposing dynamic management of the sound. A gunshot, for example, is so short in duration that there is no reasonable need to change its volume or pitch while it is playing. Instead, the system calculates all significant parameters when the sound is triggered, and these stay constant for the duration of the sound. A one-shot sound may be triggered by a call like:

```
SndPlayOneShot(sample, volume, rate, pan, loopCount);
```

When implementing sound group management, you will need to decide if it is important to support dynamic group-based control of one-shot sounds. Likely, the answer will be no, but if the system allows for uncontrolled playback of longer samples, group control may be needed.

Even if dynamic control is not needed after a sound is triggered, one-shot sounds should still be assigned to groups. Thus when the sound’s initial parameters are calculated, the group factors will be taken into account. This merely involves adding a group assignment to the sound triggering call:

```
SndPlayOneShot(sound, group, volume, rate, pan, loopCount);
```

# Portability

As with any interface wrapper you create, it is best to become familiar with all the various sound APIs that you may encounter. This will help structure your group management system to make it flexible enough to be used on a variety of platforms and with a variety of underlying sound systems. As mentioned earlier, different sound systems may take very different approaches to the management of individual playing sounds, and understanding these differences is the key to constructing a truly portable API wrapper.
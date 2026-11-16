
void OnUpdateWorldTransform() override;

SoundEvent PlayEvent(const std::string& name);

void StopAllEvents();

private:

std::vector<SoundEvent> mEvents2D;

std::vector<SoundEvent> mEvents3D;

};

The AudioComponent::PlayEvent function first calls PlayEvent on the AudioSystem. You then check whether the event is 3D to determine which of the two vectors should store the SoundEvent. Finally, if the event is 3D, call Set3DAttributes on it:

Click here to view code image

```
SoundEvent AudioComponent::PlayEvent(const std::string& name)
{
    SoundEvent e = mOwner->GetGame()->GetAudioSystem();

    // Is this 2D or 3D?
    if (e.Is3D())
    {
        mEvents3D.emplace_back(e);

        // Set initial 3D attributes
        e.Set3DAttributes(mOwner->GetWorldTransform());
    }
    else
    {
        mEvents2D.emplace_back(e);
    }

    return e;
}
```

The `AudioComponent::Update` function (omitted here) removes any of the events in `mEvents2D` or `mEvents3D` that are no longer valid. (`IsValid` returns `false`.)

Next, you add an override of `OnUpdateWorldTransform`. Recall that every time the owning actor computes its world transform matrix, it notifies each component by calling this function. For the `AudioComponent`, it needs to update the 3D attributes of any 3D events in `mEvents3D` every time the world transform changes:

**Click here to view code image**

```
void AudioComponent::OnUpdateWorldTransform()
{
    Matrix4 world = mOwner->GetWorldTransform();
    for (auto& event : mEvents3D)
    {
        if (event.IsValid())
        {
            event.Set3DAttributes(world);
        }
    }
}
```

Finally, `AudioComponent::StopAllEvents` (also omitted here) simply calls stop on every event in both vectors and clears out the vectors. The destructor of `AudioComponent` calls this function, but there may be other situations in which a game wants to just stop the sound events for an actor.

With these additions, you can attach an `AudioComponent` to an actor and play sound events on the audio component. The `AudioComponent` then automatically updates the 3D attributes of the associated events as needed.

## The Listener in a Third-Person Game

The listener directly using the camera position and orientation works great for first-person games where the camera is from the perspective of the player’s character. However, things are not quite as simple for a third-person game where the camera follows the player character. Figure 7.2 illustrates the side view of a third-person game. The player character is at position P, and the camera is at position C. Position A represents a sound effect right next to the player character. Position B is a sound effect close to the camera.

![](img/e9afcec1487716b0ef80d7e7c09869c8_527_0.png)

### Figure 7.2 Sound effects in a third-person game

Now suppose the listener uses the camera position and orientation, as in the preceding code. In this case, both sounds A and B will sound like they’re in front. This is good because both sound effects are visible onscreen, so you as the player should perceive the sounds in front. However, sound B will sound closer than sound A. This seems weird because you expect sounds right next to the player to be louder. And even if there were no sound B, any sounds right next to (or even on) the player will always have some attenuation applied to them, which may be frustrating for the sound designer.

If instead the listener uses the player position and orientation, then sound A will be louder than sound B. However, sound B then sounds like it's behind because it's positioned behind the player. This is very weird because the sound is onscreen, so you expect it to sound like it's in front.

What you effectively want is an attenuation based on the player position but an orientation based on the camera. Guy Somberg describes a great solution to this problem (his book is listed in the “Additional Reading” section at the end of the chapter), which involves just a little bit of vector math. Given the player at position P, the camera at position C, and a sound at position S, first compute two vectors—one vector from camera to sound and the other vector from player to sound:

```
PlayerToSound = S - P
CameraToSound = S - C
```

The length of the PlayerToSound vector is the desired distance for attenuation. The normalized CameraToSound vector is the correct heading. Scalar multiplying the normalized CameraToSound vector by the length of PlayerToSound yields a virtual position for the sound:

```
VirtualPos = ||PlayerToSound|| \frac{CameraToSound}{||CameraToSound||}
```

```
VirtualPos = ||PlayerToSound|| \frac{CameraToSound}{||CameraToSound||}
```

This virtual position, illustrated in Figure 7.3, yields both the correct attenuation *and* the correct orientation of the sound. The listener itself then directly uses the camera, as before.

![](img/e9afcec1487716b0ef80d7e7c09869c8_529_0.png)

### Figure 7.3 Sound effects in a third-person game with virtual positions

Note that this approach may be untenable if true world positions of sounds are necessary for other calculations (such as for occlusion, discussed later in this chapter).

## The Doppler Effect

Imagine standing on a street corner. While the police car is approaching, the pitch of the siren sound is increased. Conversely, after the police car passes, the pitch of the sound decreases. This is the Doppler effect in action, and it is illustrated in Figure 7.4.

![](img/e9afcec1487716b0ef80d7e7c09869c8_530_0.png)

### Figure 7.4 Doppler effect

The **Doppler effect** (or Doppler shift) occurs because sound waves take time to travel through the air. As the police car gets closer, each sound wave starts closer, which means the waves arrive closer together. This causes a perceived increase in frequency, leading to the heightened pitch. The true pitch of the sound is audible when the car is right next to the listener. Finally, as the car travels off, the opposite effect occurs: The sound waves arrive farther apart, yielding a lower pitch. The Doppler effect applies to all types of waves, but sound waves are the most easily observable.

In a game, the Doppler effect can create more realistic sounds for objects such as vehicles. FMOD can automatically calculate Doppler pitch shifts; it just requires passing in the correct velocities both in `setListenerAttributes` and `set3DAttributes`. This means the game likely needs a more correct physics-based movement approach with forces, as briefly discussed in Chapter 3, “Vectors and Basic Physics.”

There also are some additional Doppler parameters accessible through the Low Level API. The set3DSettings function sets these parameters:

Click here to view code image

```
mLowLevelSystem->set3DSettings(
    1.0f, // Doppler scale, 1 = normal, higher exagg
    50.0f, // How many game units = 1 meter (our game
    1.0f // (Not for Doppler, leave at 1)
);
```

## MIXING AND EFFECTS

One of the advantages of digitized sounds is that manipulation during playback is easy. You’ve already manipulated sounds as they play to account for the sound’s position relative to the listener. The term digital signal processing (DSP) refers to computational manipulation of a signal. For audio, adjusting the volume or pitch of the signal is a type of DSP.

Two other common DSP effects in games are reverb and equalization. Reverb simulates sound bouncing in an enclosed area. For example, sound effects while inside a cave have an echo because of waves bouncing off the walls. **Equalization**, on the other hand, tries to normalize the volume levels of sounds into a set range.

FMOD Studio allows configuration of chains of DSP effects. In other words, a sound can pass through multiple stages that modify the signal prior to output. Although each sound event can have its own DSP chain, a more common approach is to group sounds into types. Then, different groups can have different effects applied to them.

## Buses

In FMOD Studio, a **bus** is a grouping of sounds. For example, you might have a bus for sound effects, a bus for music, and a bus for dialogue. Each bus can individually have different DSP effects attached to it, and at runtime you can adjust buses. For instance, many games offer separate volume sliders for different categories of sound. This is straightforward to implement with buses.

By default, every project has a master bus, specified by the root path `bus:/`. However, a sound designer can add any number of additional buses. So, much as with loading in event descriptions on bank load, you can load in buses at the same time. First, you add a map of buses to `AudioSystem`:

Click here to view code image

```
std::unordered_map<std::string, FMOD::Studio::Bus*> r
```

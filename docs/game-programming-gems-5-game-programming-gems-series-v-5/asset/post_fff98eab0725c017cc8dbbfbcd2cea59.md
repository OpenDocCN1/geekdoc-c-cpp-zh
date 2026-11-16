
To be able to dynamically control the properties of a group, the system will need to update each affected sound's properties when the group's properties are changed. That is, when a call like `SndSetGroupVolume()` is made, the system will need to access and update each currently active sound that is part of the group.

In APIs that manage playing sounds as objects (not necessarily C++ objects but architectural objects), like OpenAL and DirectSound, this commonly involves keeping a list of all active sounds. When group commands are issued, the list is walked and all appropriate sounds are updated.

In "track"-based APIs, like FMod and the Miles Sound System, it is likely that your wrapper API already tracks which sounds are playing on which channels, so group management may be a bit easier to implement.

## Simplified, One-Shot Sounds

One-shot sounds are short effects that a game plays and never needs to control. Gunshots and footsteps are good examples. In many cases, wrapper APIs include simplified calls to play back one-shot sounds without exposing dynamic management of the sound. A gunshot, for example, is so short in duration that there is no reasonable need to change its volume or pitch while it is playing. Instead, the system calculates all significant parameters when the sound is triggered, and these stay constant for the duration of the sound. A one-shot sound may be triggered by a call like:

```
SndPlayOneShot(sample, volume, rate, pan, loopCount);
```

When implementing sound group management, you will need to decide if it is important to support dynamic group-based control of one-shot sounds. Likely, the answer will be no, but if the system allows for uncontrolled playback of longer samples, group control may be needed.

Even if dynamic control is not needed after a sound is triggered, one-shot sounds should still be assigned to groups. Thus when the sound's initial parameters are calculated, the group factors will be taken into account. This merely involves adding a group assignment to the sound triggering call:

```
SndPlayOneShot(sound, group, volume, rate, pan, loopCount);
```

## Portability

As with any interface wrapper you create, it is best to become familiar with all the various sound APIs that you may encounter. This will help structure your group management system to make it flexible enough to be used on a variety of platforms and with a variety of underlying sound systems. As mentioned earlier, different sound systems may take very different approaches to the management of individual playing sounds, and understanding these differences is the key to constructing a truly portable API wrapper.

## Conclusion

This simple gem shows how the concept of managing sounds in groups, in addition to at the individual level, can be useful and easy to implement. Adding this feature to a sound API wrapper may take only a few hours, yet the benefits can be far reaching. This is particularly true when the need for group-based management isn't identified early in development. Including these features in the sound API also keeps the game code base clean and allows for easier inclusion of additional features down the road.

## Using 3D Surfaces as Audio Emitters

Sami Hamlaoui

disk_disaster@hotmail.com

In games today, sound sources are represented by a single point, regardless of the type of sound being represented. Gunshots? Points. Laser beams? Two Points. Rain? Lots of points. Although this has sufficed up until now, the level of detail in games is increasing with each generation of hardware, and while technologies like EAX go some way to improving the realism of game audio, all sound still comes from an infinitely small point in 3D space. We don't want sound that comes from a point anymore—we want sound that comes from an entire surface.

This gem will show you how to create sound that appears to do just that, with almost no extra processing time required and with full hardware acceleration. Intrigued? Then read on.

### Method

Instead of using a single point as the location of the sound source, you use a standard geometric primitive such as a line, box, or sphere. Then for each frame, you calculate the closest point to the listener on the primitive and send it to the audio API as the sound's position.

This all seems rather underwhelming until you realize that as the listener moves around these emitters, the sound will travel with it. Move parallel to a line and the sound will move along with you, keeping the same distance until you move past the end of the line, at which point the sound will move behind the listener. As you walk around a sphere, the sound will appear to be a point emitter until you walk inside it and the sound comes from all directions at full volume, as if the sound is really being generated from inside the sphere itself. Use a box to represent rain outside a building, only to walk out into the open and find yourself deafened by the sound of the rain.

The best part of it all is that the sound API and the sound card still think they're working with points, meaning that the audio is accelerated on the hardware. The only thing performed in software is a closest-point algorithm, which is so simple for all the emitters that there won't be any kind of performance hit from using it!

In the following sections, four different emitters are covered: the point, line, sphere, and box. Presented alongside each description is a list of components that make up the emitter (the origin, direction, radius, etc.), the closest-point equation with a line-by-line walkthrough, and a couple of suggestions for what the emitter could be used for in a game.

### A Word on Volumes

As mentioned earlier, once the listener is inside a volume emitter (an emitter that has a definable "inside," like a sphere or box as opposed to a line or point), the sound will come from all directions at full volume. This is a deliberate part of the technique and can be used for quite a large number of special effects. They aren't listed here, as they can be found with the appropriate emitter. Suffice to say that the few examples given earlier are only the tip of the iceberg.

### A Word on the Math

In the list of components for each emitter will be the mathematical representation of the variable in the closest-point equation. However, there are a few values that will be used in each equation, and it seems daft to include them every time, so they are listed in Table 7.3.1.

| Name | Math Notation | Type |
| :--- | :--- | :--- |
| Audio Position | A | Vector |
| Listener | X | Vector |

They are defined as follows:

Audio position: This is the vector that is passed to the audio API. It is calculated by the closest-point algorithm. It is represented by A (for audio).

Listener: This is usually the camera's position. It is where the sound is currently being heard from. It is represented by X (because L is used for the line components).

Two temporary variables are used throughout the equations, too, and they also always have the same meaning. They are listed in Table 7.3.2.

| Name | Math Notation | Type |
| :--- | :--- | :--- |
| Direction | V | Vector |
| Distance | d | Scalar |

They are defined as follows:

Direction: This is the direction from something to something else. Unless stated, this value is not normalized and therefore contains distance as well as direction information.

Distance: The distance between something and something else. This is a scalar value and is usually used when projecting points towards the listener.

### Points

Table 7.3.3 shows the point components.

| Name | Math Notation | Type |
|---|---|---|
| Origin | P<sub>origin</sub> | Vector |

The first type of emitter we are going to cover is the point emitter, because although this gem focuses on alternatives, for the vast majority of the cases you need to play a sound, the point emitter will work fine. It is best if you use the other emitters when it suits the effect being created—and _only_ then. Otherwise, stick to the point.

Using a point emitter is exactly like using points for sound sources. Just set the audio position to the value of the point. As points have no properties other than their location, the closest point to the point is itself. For completeness sake, Table 7.3.3 lists components, and Equation 7.3.1 shows the nearest point on the point.

```
A = P<sub>origin</sub> (7.3.1)
```

Set the audio at the same location as the point.

### Uses

As mentioned earlier, this is useful for any small sound effect that isn't better suited to the other emitters. So, that'll be the voices, footsteps, gunshots, small explosions, rag dolls hitting things, rocket trails, fire, water dripping, etc.

### Lines

Line emitters come in two flavors: infinite lines and line segments. You will probably use the line segments most of the time, but for cases when the line is either very big or infinite, the infinite line emitter will suit you perfectly.

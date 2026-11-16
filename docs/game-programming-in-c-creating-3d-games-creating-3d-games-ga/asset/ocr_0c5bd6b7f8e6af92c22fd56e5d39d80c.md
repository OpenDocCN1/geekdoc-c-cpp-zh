player to be louder. And even if there were no sound B, any sounds right next to (or even on) the player will always have some attenuation applied to them, which may be frustrating for the sound designer.

If instead the listener uses the player position and orientation, then sound A will be louder than sound B. However, sound B then sounds like it's behind because it's positioned behind the player. This is very weird because the sound is onscreen, so you expect it to sound like it's in front.

What you effectively want is an attenuation based on the player position but an orientation based on the camera. Guy Somberg describes a great solution to this problem (his book is listed in the “Additional Reading” section at the end of the chapter), which involves just a little bit of vector math. Given the player at position P, the camera at position C, and a sound at position S, first compute two vectors—one vector from camera to sound and the other vector from player to sound:

```
PlaerToSound = S - P
CameraToSound = S - C
```

The length of the PlayerToSound vector is the desired distance for attenuation. The normalized CameraToSound vector is the correct heading. Scalar multiplying the normalized CameraToSound vector by the length of PlayerToSound yields a virtual position for the sound:
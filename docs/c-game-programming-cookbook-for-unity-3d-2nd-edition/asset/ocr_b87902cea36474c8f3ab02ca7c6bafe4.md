```
public SoundObject(AudioClip aClip, string aName,
float aVolume, AudioMixerGroup theMixer, Transform myParent)
{
    sourceGO = new GameObject("AudioSource." + aName);
    sourceGO.transform.parent = myParent;
}
```

Above, the constructor of the SoundObject class (a function that runs automatically when SoundObject is instantiated) contains set up code to be create a new GameObject in the Scene for its AudioSource Component to be attached to. When playing sounds, we do not call SoundObject directly – this is done further down, by the BaseSoundManager class. Note that the constructor for SoundObject has 5 parameters – when a SoundObject instance is created, each one will need these parameters passed into it. You will see how this is done further down in the BaseSoundManager class.

The constructor starts by creating a new GameObject with new GameObject(), which takes a name as a parameter – naming the new GameObject based on this. To make sure we know what this GameObject is, in the Scene's Hierarchy, it is named AudioSource followed by a name passed into this constructor as a parameter. Next, we set the parent of the new GameObject here, too, or more specifically the parent of its Transform. This is all about keeping sound GameObjects together in the Scene to keep it all neat and tidy and we get the parent Transform from a passed in parameter named myParent.

```
sourceTR = sourceGO.transform;
source = sourceGO.AddComponent<AudioSource>();
source.outputAudioMixerGroup = theMixer;
source.playOnAwake = false;
source.clip = aClip;
source.volume = aVolume;
source.maxDistance = 2000;
}
```

Every time we want to set the position of a sound, we will need to access the Transform of this GameObject and we store a reference to the Transform in the variable sourceTR, so that we do not have to look up the Transform repeatedly.

Next, we add an AudioSource to our new GameObject with GameObject.AddComponent(). We keep a reference to the AudioSource in the variable source for easy access later, and so that we can set the relevant properties on it, above. The properties we set on the AudioSource are:

+   - **outputAudioMixerGroup** – This is the Audio Mixer for the sound to play through (passed in as a parameter).
+   - **playOnAwake** – We set this to false, to prevent the AudioClip from playing automatically.
+   - **Clip** – This is the AudioClip (the sample) that will be played by this AudioSource.
+   - **Volume** – Our volume levels will usually be controlled by the AudioMixers, but having the volume available provides an extra method for individual audio volume control, if needed.
+   - **maxDistance** – This is the maximum distance at which our sound should be heard.
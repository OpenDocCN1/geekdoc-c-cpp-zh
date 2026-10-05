# Unity Games by Tutorials

soundEffectAudio refers to the audio source you added to the SoundManager earlier that will be used to play sound effects. Since you won't need to adjust the second audio source that plays background music in code, there's no reason to create a reference for it.

Next, add the following to Start():

```
if (Instance == null)
{
    Instance = this;
} else if (Instance != null)
{
    Destroy(gameObject);
}
```

This is a simple coding design pattern, known as a singleton pattern, that ensures there is always only one copy of this object in existence. If this is the first SoundManager created, it sets the Static variable to the current object. If, for some reason, a second SoundManager is created, it automatically destroys itself to make sure that there is only one SoundManager exists.

Next, add the following after the last bit of code:

```
AudioSource[] sources = GetComponents<AudioSource>();
foreach (AudioSource source in sources)
{
    if (source.clip == null)
        soundEffectAudio = source;
}
```

You need to get a handle to the AudioSource component you added to the SoundManager that you'll use to play sound, but currently you have two Audio Source components on the GameManager. How can you find the correct one? One way is to search through all the Audio Source components for the one you're looking for. GetComponents() returns all of the components of a particular type. Although Unity tends to return components in the same order as they are in the Inspector, you shouldn't count on that as behavior may change. Instead, you should look for something that distinguishes the one you're looking for. In this case, since you added music to one of the sources, this checks for the audio source that has no music before setting soundEffectAudio.

Now you're going to build your sound effects library.

Add the following instance variables after the class definition:

```
public AudioClip gunFire;
public AudioClip upgradedGunFire;
```

![](bbox=[0.118, 0.933, 0.255, 0.953])
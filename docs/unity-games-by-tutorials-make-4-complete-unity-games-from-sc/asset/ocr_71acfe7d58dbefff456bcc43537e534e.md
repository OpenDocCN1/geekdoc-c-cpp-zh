# Playing sounds

In the Hierarchy, expand the SpaceMarine and select BobbleMarine-Body. In the Inspector, click the Add Component button, and select Audio Source from the Audio category.

Next, double-click the Gun script to edit it and add the following instance variable:

```
private AudioSource audioSource;
```

Add the following to Start():

```
audioSource = GetComponent<AudioSource>();
```

This just gets a reference to the attached AudioSource — you'll be using this lot. In fireBullet(), add the following PlayOneShot before the closing brace:

```
audioSource.PlayOneShot(SoundManager.Instance.gunFire);
```

This code plays the shooting sound.

Note that there are two ways to play sound effects via code in Unity:

+   - PlayOneShot(), as you've used here, allows the same sound to play multipiple at once, overlapping the sound. For example, the space marine could shoot one bullet, and while the sound effect for that was still playing, the space marine could quickly fire another bullet, and while you'd hear both sound effects at once. The space marines fires quickly, so this is what we want, here.
- Play() only allows the sound effect to play a single time at once. If you play a sound effect, and then call Play() again, it will restart the sound, making the first effect sound like it was cut out. The advantage of Play() over PlayOneShot() is that Play() can be stopped in progress whereas PlayOneShot() cannot.

Save the file and go back to Unity. Play your game and fire that gun to hear the shooting sounds.

It's sounding awesome, but it is a bit disappointing that you don't hear the aliens die when you blast them away. So you will add the sound for the next.

Note that you can't make the alien play its own sound as you did for the bullet, because when an alien dies, you destroy the Alien GameObject. When you destroy a GameObject, any sounds playing on an AudioSource stop instantly.
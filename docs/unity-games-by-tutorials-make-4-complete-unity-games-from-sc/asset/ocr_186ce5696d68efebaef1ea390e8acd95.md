# Unity Games by Tutorials

# Chapter 7: Sound

![](bbox=[0.238, 0.088, 0.762, 0.287])

Click the **gear icon** again, and in this time, select **Remove Component**. Finally, select the **SoundManager** in the Hierarchy and find any component in the Inspector.

Click the **gear icon** and choose **Paste Component as New.**

![](bbox=[0.238, 0.387, 0.762, 0.592])

Now you have two audio sources. The first plays sound effects, while the second plays the background music.

Click the **Add Component** button and select **New Script**. Name it **SoundManager** and then click **Create and Add**. Open the script in your code editor.

You to be able to access this script anywhere in your game. After the opening brace, add the following:

```
public static SoundManager Instance = null;
private AudioSource soundEffectAudio;
```

Instance will store a static reference to the single instance of SoundManager. This will be handy so you can quickly get a reference to the SoundManager anywhere in your scripts, without having to go through the normal process of making a public variable that you set in the Unity editor.

![](bbox=[0.125, 0.932, 0.285, 0.952])

189
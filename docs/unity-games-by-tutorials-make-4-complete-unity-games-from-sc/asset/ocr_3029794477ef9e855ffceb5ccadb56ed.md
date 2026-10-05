# Playing background music

Select Main Camera in the Hierarchy. Click the Add Component button and select Audio Source in the Audio category.

![](bbox=[0.303, 0.191, 0.703, 0.436])

You're adding the Audio Source for the background music to the camera, since that's the same place the audio listener. This way, the volume of the background music will always stay the same; think of it carrying around your own boom box!

As you can see, you have an array of options. Here's the breakdown:

+   * AudioClip: The actual sound file. You create a clip by dragging a sound file into Unity, and then the engine converts it to an audio clip. In your case, you imported the sounds when you imported the models in Chapter 1, "Hello, Unity."

> > Pro Tip: Avoid formats such as MP3 because Unity sometimes re-encodes compressed files to a lower quality when it exports the game. To avoid this, we have provided the audio as OGG files.

+   * Output: This represents the Audio Mixer to use. You'll learn what this means later in this chapter.

+   * Mute: Check if you'd like to mute the audio. This can be useful to programmatically mute sounds mid-game or disable sounds while testing.

+   * Bypass Effects/Listener/Reverb Zones: Turns off any additional effects that you might add to a sound. Effects can add depth and increase realism. For instance, consider the difference between footsteps in a cavernous structure with and without an echo.